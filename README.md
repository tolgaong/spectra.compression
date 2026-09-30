# Spectra.Compression

Fast, secure, streaming-first compression and archive processing for .NET.

Spectra.Compression is a managed compression toolkit for applications that need
codec, container, and archive support with explicit interoperability and
resource-safety boundaries. The product targets .NET 8 and .NET 10. Support is
format-specific; the detailed matrix documents where APIs are incremental,
metadata-first, or complete-buffer conveniences.

## Current status

The product projects define a 1.0 package line, but the packages are not
currently available from NuGet.org. Do not infer availability from package
names or local build metadata. Installation instructions will be added when a
public release is promoted.

## Format overview

| Area | Current support |
|---|---|
| Deflate, gzip, and zlib | Encode, decode, and incremental streaming |
| Brotli | Encode, decode, and incremental streaming |
| Zstandard | Encode, decode, dictionaries, seekable frames, and incremental streams |
| LZ4 | Frame/raw/legacy support and incremental standard-frame streams |
| Bzip2 | Encode, decode, concatenated members, and incremental streams |
| XZ and LZMA/LZMA2 | Encode/decode; public streaming boundaries vary by API |
| ZIP | Read/write plus metadata-first streaming for selected unencrypted methods |
| 7z | Read/write subsets plus metadata-first streaming for selected seekable archives |
| RAR | Evidence-backed partial decode only; no writer |

See [Supported formats](docs/supported-formats.md) for the exact coverage and
limitations. In particular, Spectra.Compression does not claim complete support
for every historical or modern RAR variation.

## Streaming and safety

Streaming APIs use one of four explicit models: true incremental codec
streaming, metadata-first archive streaming, bounded adapters, or
complete-buffer convenience APIs. For incremental paths, retained memory is
intended to follow codec state, dictionary/window size, bounded buffers, and
container state rather than file size. This is a bounded-memory design goal,
not a zero-allocation claim.

Compressed input is treated as hostile. Supported paths validate sizes,
structure, checksums, and declared limits. Archive consumers should retain
output, expansion-ratio, entry-count, and nesting limits and should keep safe
path handling enabled. Read [Streaming](docs/streaming.md) and
[Archive safety](docs/archive-safety.md) before processing untrusted data.

## Documentation

- [Getting started](docs/getting-started.md)
- [Packages](docs/packages.md)
- [Supported formats](docs/supported-formats.md)
- [Streaming](docs/streaming.md)
- [Compatibility](docs/compatibility.md)
- [Archive safety](docs/archive-safety.md)
- [Benchmark publications](docs/benchmarks/README.md)
- [Public roadmap](ROADMAP.md)
- [Security policy](SECURITY.md)
- [Support policy](SUPPORT.md)

## Benchmarks

No benchmark numbers are published in this bootstrap. Future reports will be
release-linked, workload-specific, and accompanied by reproducible methodology.
See the [benchmark publication policy](docs/benchmarks/README.md).

## Support and issues

Use [GitHub Issues](https://github.com/tolgaong/spectra.compression/issues) for
reproducible bugs, compatibility reports, documentation problems, and feature
requests. Do not attach private archives, passwords, tokens, or other secrets.
See [SUPPORT.md](SUPPORT.md) for triage principles and [SECURITY.md](SECURITY.md)
for vulnerability reporting.

## Source availability

This repository hosts the public documentation, examples, benchmark results,
release information, and issue tracking for Spectra.Compression. The
implementation source is not published in this repository.

## License

The public documentation in this repository is provided under the
[MIT License](LICENSE).
