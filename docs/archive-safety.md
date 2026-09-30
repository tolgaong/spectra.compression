# Archive Safety

Compressed and archived input should be treated as hostile. Safety depends on
selecting a supported format shape and retaining explicit policies at the
application boundary.

## Paths and links

- Reject absolute paths, rooted paths, drive-qualified paths, and traversal
  segments such as `..` before writing.
- Resolve output paths beneath a dedicated extraction root and verify that the
  resolved destination remains inside that root.
- Keep safe path handling enabled. Do not enable unsafe compatibility modes for
  untrusted archives.
- Treat symbolic and hard links as separate capabilities. Reject or skip them
  unless the application has an explicit, containment-preserving link policy.

## Resource limits

- Enforce maximum total output and maximum single-entry output before writing.
- Enforce an expansion-ratio limit when compressed size is known.
- Bound entry counts and archive nesting.
- Validate dictionary, window, table, metadata, and declared-size limits before
  allocating.
- Remember that disabling limits can turn a valid but adversarial archive into
  a decompression bomb.

## Validation and malformed input

Reject truncated headers, invalid offsets, unsupported variants, ambiguous
metadata, incorrect checksums, and size mismatches. Do not continue with a
nearby codec or format interpretation after validation fails. For streaming
archives, a terminal failure may invalidate later solid-dependent entries.

## Passwords and encrypted archives

- Do not log passwords, keys, decrypted content, or sensitive filenames.
- Keep credentials out of command lines, issue reports, and progress messages.
- Clear mutable temporary secret buffers when ownership permits it.
- Recognize that several historical archive encryption schemes, 7z AES-CBC,
  and RAR AES-CBC are not authenticated encryption. Wrong passwords or
  corruption may be distinguishable only through structure, decoder failure,
  size checks, or CRCs.
- ZIP encrypted-entry support is currently a complete-buffer compatibility
  path, not metadata-first streaming.

## Cancellation and integrity

Pass cancellation through async reads, writes, KDF work, and extraction loops.
Cancellation is a failed/incomplete operation: remove or quarantine partial
destination files according to application policy.

Always require the documented checksum, CRC, declared-size, and structural
validation to finish. Bytes emitted before a terminal checksum succeeds should
not be published as trusted output.
