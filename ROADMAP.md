# Spectra.Compression Public Roadmap

Roadmap items describe intended product work, not current capability or a
delivery commitment. Items have no promised dates and may be reordered when
correctness, security, interoperability, or release evidence requires it.

| Item | Status | Direction |
|---|---|---|
| Release Candidate Readiness & Package Consumption Hardening | Planned | Validate public package consumption, metadata, documentation, provenance, and release controls. |
| Benchmark Baseline & Performance Contract | Planned | Establish reproducible workloads, machine disclosure, regression criteria, and release-linked reports. |
| Unified Archive Detection / High-Level API | Investigating | Evaluate a stable format-detection and archive-opening surface without hiding format-specific safety boundaries. |
| High-Level Extraction & Policy Layer | Investigating | Define destination, overwrite, path, link, limit, cancellation, and failure semantics before adding convenience APIs. |
| CLI | Investigating | Explore a bounded command-line adapter over stable product APIs. |
| Remote / Storage Providers | Investigating | Explore capability-focused adapters for remote and object-storage sources without coupling codecs to infrastructure. |
| Observability & Resource Governance | Investigating | Extend progress and diagnostics while preserving deterministic output and bounded resource policies. |

Completed capabilities are documented in [Supported formats](docs/supported-formats.md),
not inferred from this roadmap.
