# Getting Started

## Package availability

Spectra.Compression packages are not currently published on NuGet.org. The
package names and APIs below describe the current product surface, but there is
no supported public installation command yet. This page will gain verified
package references when a release is promoted; no version should be inferred
from repository content.

The supported target frameworks are .NET 8 and .NET 10.

## Choose an API by workload

- Prefer a true incremental stream for large or unknown-length codec payloads.
- Prefer a metadata-first archive reader when its documented format subset
  covers the archive.
- Use complete-buffer convenience APIs only when materializing the input and
  output is acceptable under explicit limits.
- Keep decompression limits and safe archive-path handling enabled for
  untrusted input.

## gzip stream

The following example uses the current `SpectraGZipStream` constructor:

```csharp
using spectra.compression.gzip;
using System.IO.Compression;

await using var input = File.OpenRead("data.txt");
await using var output = File.Create("data.txt.gz");
await using var gzip = new SpectraGZipStream(
    output,
    CompressionMode.Compress,
    leaveOpen: false);

await input.CopyToAsync(gzip, cancellationToken);
```

## Zstandard streaming decode

This example uses the current bounded decode stream and shared limits contract:

```csharp
using spectra.compression;
using spectra.compression.zstd;

await using var input = File.OpenRead("data.zst");
await using var decoder = new ZstdDecodeStream(
    input,
    dictionary: null,
    DecompressionLimits.Default,
    leaveOpen: false,
    progress: null);
await using var output = File.Create("data.bin");

await decoder.CopyToAsync(output, cancellationToken);
```

`ZstdFrameDecoder.DecodeAll` remains a complete-buffer convenience API. Use
`ZstdDecodeStream` when the compressed source or decoded result may be large.

## Before archive extraction

Review [Supported formats](supported-formats.md), [Streaming](streaming.md), and
[Archive safety](archive-safety.md). Do not substitute a high-level API name
from a future roadmap item; for example, no `SpectraArchive.OpenAsync(...)` API
is documented or promised here.
