# Benchmark Methodology

This document defines how a future Spectra.Compression benchmark publication
is produced and interpreted. It contains methodology only; no competitive
measurements have been approved or published.

## Publication boundary

Benchmark code, raw results, environment captures, correctness records, and
engineering analysis remain in the private source repository. A run is
`internal-only` by default. It may become a `publication-candidate` only after
private validation and analysis, and it may become `published` only after
explicit human review and a separate public-repository commit.

There is no automatic private-to-public synchronization, commit, or push.
Publication staging is review material and cannot itself establish approval.

## Workloads and corpus

The initial deterministic synthetic corpus covers highly compressible or
repeating data, natural-language text, structured JSON-like text, mixed binary
data, and seeded incompressible pseudorandom data. Micro/codec sizes are 1 KiB,
64 KiB, 1 MiB, and 16 MiB. Large streaming and retained-memory scenarios use
256 MiB logical payloads selectively rather than multiplying that size across
every parameter combination.

Archive corpora distinguish many small files, one large file, mixed sizes,
compressible entries, and incompressible entries. Genuine or
reference-produced fixtures are used when archive semantics require them.
Each promoted report identifies its corpus revision, seeds, sizes, and SHA-256
hashes. Any external corpus must also disclose source, license, redistribution
permission, and acquisition hash or recipe.

## Correctness before performance

A measurement is eligible only after its case passes the applicable check:

- encoded output is independently decoded and compared byte for byte;
- canonical compressed input is decoded and compared byte for byte;
- archive entry count, names where applicable, sizes, hashes, and integrity are
  verified; and
- streaming output and claimed early-output behavior are verified.

An incorrect case is reported as INVALID and has no timing result. An operation
that the implementation does not expose or claim is N/A/UNSUPPORTED, not a
zero or a loss.

## Fair comparisons

Encode participants receive identical raw input. Decode participants receive
the same canonical interoperable compressed artifact wherever the format
permits it, so encoder output differences do not contaminate decode throughput.

Configurations match underlying semantics as closely as the APIs allow.
Reports disclose actual compression levels or quality, window/dictionary and
block sizes, frame/container options, checksums, content-size behavior,
independent or linked blocks, and flush/finalization choices. Labels such as
“Fastest,” “Optimal,” “Default,” and “Level 1” are not treated as equivalent
without evidence.

Raw Deflate and GZip, LZ4 block and frame, raw LZMA, LZMA2, and XZ are distinct
workloads. Archive reporting likewise keeps open/metadata, enumerate, extract
one, extract all, and streamed entry consumption separate.

Corpus generation, fixture construction, validation hashing, logging, result
serialization, and unrelated process startup are excluded from timed bodies.
Construction or archive-open cost is measured separately when it is the user
operation of interest.

## Metrics

Codec reports may include encode/decode latency, raw-logical-byte throughput in
MiB/s, managed allocation and GC collections per operation, encoded byte count,
and `compressed_size / original_size` ratio (with optional `1 - ratio` space
saving). Streaming reports additionally disclose consumer buffer size, time to
first caller-visible output, total throughput, allocation, source-read
behavior, and flush/finalization cost.

Isolated-process memory scenarios supplement managed-allocation diagnostics
with post-GC retained managed delta, working set, peak working set,
dictionary/window and explicit codec state, buffers, and archive entry/volume
counts. The objective is to test whether supported bounded streaming scales
with codec/container state rather than complete logical input, prior solid
outputs, or multipart volume count.

Results are reported per workload and metric. Spectra.Compression does not use a synthetic overall score because throughput, compression ratio, latency, allocation, and memory usage represent different trade-offs.

An Overall page provides navigation, release/build and machine context,
workload and metric summaries, and links to detailed reports. It does not
calculate a combined score, weighted points, one universal winner, or a
geometric mean across semantically unrelated workloads. Charts, when useful,
retain their numeric table or machine-readable source and never combine
unrelated units on one axis.

## Environment and repeatability

Every promoted snapshot identifies UTC timestamp and run ID, source and
benchmark commits, dirty/clean state, runtime and SDK, operating system and
kernel/build, architecture and process architecture, CPU and logical/physical
core counts, RAM, virtualization, available power/governor information,
benchmark harness version, competitor package versions, corpus revision,
profile, and command line.

Selected cases are repeated and report sample count, mean, median, standard
deviation, and confidence/error information when available. Differences below
the observed noise floor are not interpreted. Virtual-machine data may support
internal regression and harness validation, but it is not automatically a
canonical public competitive environment. Public release results should
prefer a stable physical or otherwise explicitly controlled host.

## Comparison candidates

Initial comparison candidates are System.IO.Compression, SharpCompress,
SharpZipLib, ZstdSharp.Port, ZstdNet, and K4os.Compression.LZ4.Streams. Each
report gives exact versions, licenses, supported operations, runtimes and
architecture restrictions, and whether an implementation is fully managed,
wraps native code, P/Invokes an external codec, or bundles native binaries.
Managed and native models are methodology context; neither is inherently
better or worse. Listing a library does not imply endorsement or affiliation.

No library is compared on a format or operation it does not support. The
initial format coverage is Deflate, GZip, Brotli, Zstandard, LZ4 frames, BZip2,
ZIP, 7z, RAR, and genuinely comparable XZ/LZMA-family operations.

## Interpretation and selective publication

Published values must derive exactly from the reviewed private run. A report
may omit an entire experimental section, but it must disclose the workload and
configuration that it does publish, document methodological exclusions, and
must not remove an implementation merely because it performed better. It must
not imply that an unpublished workload was won.

Claims are scoped to the disclosed payload, settings, runtime, and machine.
They should say “On this disclosed workload” or “In this benchmark,” and expose
trade-offs such as speed versus ratio, allocation, or first-output latency.
Benchmark baselines are observations, not universal performance promises or
public service-level agreements.
