# Compatibility

Compatibility claims are limited to documented formats, API shapes, and
interoperability evidence. A valid archive can still use a feature outside the
supported subset.

## Runtime baseline

Product packages target .NET 8 and .NET 10. `netstandard2.0`, .NET Framework,
and other target frameworks are not promised. Public codec and stream instances
are mutable and should not be shared concurrently; separate instances can run
independently.

## Important boundaries

- ZIP metadata-first streaming supports Store, Deflate, Deflate64, Bzip2, and
  ZIP-LZMA without encryption. Data descriptors require seekable input.
- 7z metadata-first streaming requires seekable input and supports selected
  raw-header Copy/Deflate/LZMA/LZMA2 pipelines, including specific linear AES
  pipelines. Encoded headers and arbitrary coder graphs remain outside that
  streaming surface.
- XZ decode is incremental internally, but there is no public source-stream
  adapter.
- Bzip2 randomized legacy blocks are rejected.
- LZ4 dictionary IDs are exposed as metadata, but external dictionary bytes are
  not accepted by the frame or stream APIs.
- RAR is a partial reader with exact evidence-backed generation, encryption,
  solid, multipart, metadata, and recovery boundaries. It is not a writer or a
  general archive-repair tool.
- Complete-buffer compatibility APIs may be unsuitable for large or untrusted
  payloads even when their format shape is supported.

Unsupported or ambiguous inputs should fail deterministically rather than
silently changing format semantics. Submit a compatibility report with the
producing implementation, command/options, smallest safe sample, and expected
behavior when possible.
