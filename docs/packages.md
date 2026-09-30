# Packages

All current product projects target `net8.0` and `net10.0`. The package IDs
below are defined by the product source, but none is currently available from
NuGet.org. No `Spectra.Compression.Common` package exists.

| Package / project | Purpose | TFMs |
|---|---|---|
| `Spectra.Compression` | Core DEFLATE/Deflate64, LZMA/LZMA2, Snappy, LZFSE, checksum, cryptographic, filter, and stream primitives | `net8.0`; `net10.0` |
| `Spectra.Compression.Brotli` | RFC 7932 Brotli encode/decode and incremental stream adapter | `net8.0`; `net10.0` |
| `Spectra.Compression.Bzip2` | Bzip2 encode/decode, concatenated members, CRC validation, and incremental streams | `net8.0`; `net10.0` |
| `Spectra.Compression.Gzip` | gzip encode/decode streams, multi-member decode, and parallel chunk encoding | `net8.0`; `net10.0` |
| `Spectra.Compression.Lz4` | LZ4 frame, raw-block, legacy-frame, LZ4HC, and incremental standard-frame streams | `net8.0`; `net10.0` |
| `Spectra.Compression.Rar` | Partial, evidence-backed RAR compatibility and streaming decode; no writer | `net8.0`; `net10.0` |
| `Spectra.Compression.Tar` | TAR read/write, metadata-first reading, compressed wrappers, and path/link policies | `net8.0`; `net10.0` |
| `Spectra.Compression.SevenZip` | 7z compatibility read/write and selected metadata-first streaming decode | `net8.0`; `net10.0` |
| `Spectra.Compression.Xz` | XZ/LZMA2 encode/decode with registered Delta and BCJ decode filters | `net8.0`; `net10.0` |
| `Spectra.Compression.Zip` | ZIP/ZIP64 read/write, encryption compatibility, and selected metadata-first streaming decode | `net8.0`; `net10.0` |
| `Spectra.Compression.Zstd` | Zstandard frames, dictionaries, checksums, seekable support, and encode/decode streams | `net8.0`; `net10.0` |

Package availability, supported APIs, and format coverage are separate facts.
Check [Getting started](getting-started.md) for release status and
[Supported formats](supported-formats.md) for behavior boundaries.
