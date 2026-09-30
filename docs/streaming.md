# Streaming

Spectra.Compression uses explicit streaming models so callers can choose an API
whose latency and memory behavior match the workload.

## True incremental streaming

An incremental codec advances as input arrives and output space becomes
available. It does not require the complete logical payload before progress.
Current public incremental paths include Deflate/zlib/gzip, Brotli, Snappy
framed streams, Zstandard, LZ4 standard frames, and Bzip2. Deflate64 also has a
partial-buffer codec API and is used by the ZIP streaming reader.

Stream and codec instances are stateful and are not thread-safe. Keep one
instance for one operation, honor consumed/written counts, drain output when
requested, and treat terminal validation or I/O failures as terminal.

## Metadata-first archive streaming

A metadata-first reader exposes one entry's metadata before its content stream.
The entry content is then consumed sequentially without materializing the whole
entry. ZIP, TAR, selected 7z, and evidence-backed RAR subsets provide this model.

Formats may require seekability or bounded preparation. ZIP data descriptors
need a seekable source. The 7z reader supports selected seekable raw-header
coder graphs. Some solid 7z and RAR operations must decode and discard earlier
content to establish valid history before exposing a later entry.

Advancing with an unfinished entry may require bounded drain or may be rejected.
Any prerequisite decode, limit, checksum, cancellation, or I/O failure can
invalidate dependent entries.

## Bounded adapters

Some APIs incrementally process an internal pipeline while retaining a bounded
block, dictionary, window, metadata index, crypto block, or filter region.
“Bounded” does not mean allocation-free, and the bound can be material—for
example, it may include a codec dictionary selected by the input format.

XZ currently uses bounded incremental decode internally, but its public source
input remains a complete `byte[]`; it is therefore not presented as a public
source-stream API.

## Complete-buffer convenience APIs

APIs returning a `byte[]` or a list of entry payloads necessarily materialize
their results and may also require complete input. They are useful for small,
trusted, explicitly bounded payloads. They should not be substituted for a
streaming API when file size is unbounded or attacker-controlled.

## Memory guidance

For documented incremental paths, retained memory should scale with:

- codec state;
- dictionary or history-window size;
- bounded input, output, crypto, and filter buffers;
- bounded container and entry state.

It should not scale with total file size. Cumulative allocation, CPU work, and
I/O can still scale with input size, the number of entries or volumes, flush
frequency, and solid-prefix drain. No zero-allocation claim is made.

## Cancellation, progress, and integrity

Supported async streaming paths accept cancellation. Cancellation is not a
successful archive boundary and can poison state that depends on partially
decoded history. Optional progress reporting must not change output,
validation, or limit behavior.

Checksums and authentication boundaries can be terminal. A streaming consumer
may receive bytes before a final checksum or unauthenticated legacy-encryption
failure is known. Do not treat streamed bytes as validated until the entry or
stream completes successfully.
