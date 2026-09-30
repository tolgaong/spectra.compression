# Benchmark Publications

This directory is the public landing page for deliberately promoted benchmark
reports. No benchmark numbers are published in this bootstrap.

## Publication boundary

The private source repository retains benchmark code, harness implementation,
raw results, machine-local artifacts, and internal regression analysis. This
public repository receives only explicitly promoted reports, reproducible
methodology, and selected results tied to a release or named candidate.

There is no automatic publish or synchronization path from private benchmark
results to this repository. Each report must be reviewed for accuracy,
reproducibility, provenance, sensitive paths, and suitability for public use.

## Reporting principles

Results are reported per workload and metric. Spectra.Compression does not use a synthetic overall score because throughput, compression ratio, latency, allocation, and memory usage represent different trade-offs.

Every published result should identify:

- the product package and exact release or candidate identity;
- runtime, operating system, architecture, CPU, and relevant power settings;
- input corpus provenance, size, content class, and hashes where distributable;
- codec/archive options, dictionary/window settings, and concurrency;
- warmup, iteration, isolation, and measurement procedure;
- throughput, latency, compression ratio, managed allocation, and retained or
  peak memory when applicable;
- comparison implementation and version when a comparison is made;
- known limitations and whether the workload is synthetic or representative.

Correctness and interoperability checks must pass before performance results
are promoted. Results are observations for disclosed workloads and machines,
not universal promises.

## Anticipated report structure

- **Overall:** navigation and release context, not a synthetic score.
- **Compression codecs:** workload-specific encode/decode measurements.
- **Archive formats:** format operations with integrity and feature context.
- **Streaming:** first-output behavior, buffer sizes, throughput, and flush cost.
- **Memory:** allocations, retained state, peak working set, and limits.
- **Methodology:** environment, corpora, commands, validation, and analysis.
