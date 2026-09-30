# Supported Formats

This matrix describes the current product capability, including important
public-streaming boundaries. “Partial” means only the documented subset is
supported; it is not a claim about adjacent variants.

| Format | Encode | Decode | Public streaming | Archive / container use | Important limitations |
|---|---|---|---|---|---|
| Deflate | Yes | Yes | True incremental encode/decode | gzip, zlib, ZIP, and selected 7z paths | Raw Deflate has no integrity checksum of its own. |
| Deflate64 | Yes | Yes | Incremental codec API; ZIP entry decode | ZIP method 9 | No dedicated standalone `Stream` wrapper. |
| gzip | Yes | Yes | True incremental encode/decode | gzip container, including multi-member decode | One mutable stream instance per operation. |
| zlib | Yes | Yes | True incremental encode/decode | RFC 1950 envelope over Deflate | One mutable stream instance per operation. |
| Brotli | Yes | Yes | True incremental encode/decode | Standalone RFC 7932 streams | `DecodeAll` and encode conveniences materialize complete payloads. |
| Zstandard | Yes | Yes | True incremental encode/decode | Standard, concatenated/skippable, dictionary, and seekable frames | Streaming encode uses block-local matching; frequent flushes can reduce ratio. |
| LZ4 | Yes | Yes | True incremental standard-frame encode/decode | Standard, concatenated/skippable, raw-block, and legacy forms | External dictionary bytes are not accepted; dictionary ID is metadata only. Raw/legacy conveniences materialize. |
| Bzip2 | Yes | Yes | True incremental encode/decode | Standalone and ZIP/TAR integrations | Randomized legacy blocks are rejected. Compatibility array APIs materialize. |
| Snappy | Yes | Yes | True incremental framed streams | Raw and framed forms | Raw-block APIs are complete-buffer conveniences. |
| XZ | Yes | Yes | No public source-stream adapter | XZ container with LZMA2 and registered Delta/BCJ filters | Decode is incremental internally, but public input remains a complete `byte[]`. |
| LZMA / LZMA2 | Yes | Yes | No general-purpose public stream adapter | ZIP-LZMA, selected 7z folders, and XZ internals | Raw public convenience APIs materialize complete results. |
| LZFSE | No | Yes | No | Raw, LZVN, `bvx1`, and `bvx2` decode paths | Decoder only; public decode is complete-buffer oriented. |
| ZIP | Yes | Yes | Partial metadata-first read | Store, Deflate, Deflate64, Bzip2, ZIP-LZMA, ZIP64, and encryption compatibility | Streaming covers unencrypted listed methods. Descriptors require seekable input; encrypted streaming and archive streaming write are unavailable. |
| TAR | Yes | Yes | Metadata-first read | USTAR, PAX, GNU extensions, and compressed wrappers | No public archive streaming writer. Links require explicit policy. |
| 7z | Subset | Yes | Partial metadata-first read | Copy, Deflate, LZMA/LZMA2, AES, and documented coder graphs | Streaming requires seekable input and raw headers; encoded headers, filters, BCJ2/multi-packed and arbitrary branching graphs are excluded. Encrypted writing is not claimed. |
| RAR | No | Partial | Partial metadata-first read | Fixture-proven early, later legacy, and RAR 5 subsets | No writer. No `UNP_VER=26`; historical, solid, encrypted, multipart, authenticity, and recovery support is limited to exact documented evidence-backed shapes. |

## RAR scope

RAR support is deliberately conservative. Proven decode paths include selected
RAR 1.40.2 and WinRAR 1.54 Unpack15 data, selected RAR 2.x Unpack20 data,
fixture-proven later legacy Unpack29 shapes, and selected RAR 5 stored and
algorithm-version-0 Huffman/LZ77/filter shapes. Exact supported subsets include
specific solid, encrypted, multipart, historical metadata, and single-shard
embedded-recovery cases.

The product does not claim universal historical RAR support, cryptographic
authenticity verification, generic parity repair, automatic volume discovery,
external `.rev` recovery, or RAR creation. Unknown or unproven combinations
must fail rather than be interpreted as a nearby supported variant.

See [Compatibility](compatibility.md), [Streaming](streaming.md), and
[Archive safety](archive-safety.md) before selecting an API.
