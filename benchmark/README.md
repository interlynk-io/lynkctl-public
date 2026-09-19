# Embedded firmware SBOM benchmark

This directory holds the benchmark protocol. **No comparative benchmark results are published yet.** The two [example SBOMs](../examples/sboms/README.md) establish reproducible inputs and output inspection, not accuracy or performance rankings.

## Corpus and ground truth

Start with the pinned FreeRTOS configurations in the example provenance files. Expand across independent public firmware projects, MCU families, and build providers before making broad claims. For every case, record the upstream URL, commit, submodule revisions, license references, exact target/configuration, prerequisites, compiler/linker versions, and artifact/map hashes.

Create a manually reviewed expected-component inventory from the selected build and source evidence. Record expected name, version, license, inclusion/scope, supporting file and lines, and uncertainty. Source-tree presence alone is not proof of shipment. Review ground truth independently of any generator's output.

## Comparable runs

1. Pin each generator version and checksum, command, configuration, and enrichment database revision/hash.
2. Separate metadata-only runs from runs with actual build/linker artifacts. Separate offline from network-enriched runs.
3. Use the same evidence for every tool; report unsupported inputs and errors explicitly.
4. Preserve raw SBOMs, stderr, exit codes, schema-validation reports, environment details, and file hashes.
5. Measure setup separately. Report cold-cache and warm-cache runs separately; run at least five measured repetitions per configuration, publishing all measurements, median, and range.
6. Repeat generation with a fixed timestamp and checkout path to test byte stability.

## Metrics

| Metric | Definition |
| --- | --- |
| Component precision | Correctly identified expected components / identified components, under a documented identity-matching policy |
| Component recall | Correctly identified expected components / ground-truth components |
| Version/license accuracy | Correct values / ground-truth components with independently verified values; report missing values separately |
| Scope accuracy | Correct inclusion/exclusion against the selected linked artifact; only for cases with ground truth |
| Provenance coverage | Identified components with inspectable evidence / identified components |
| Schema validity | Official schema pass/fail, independently of metadata completeness |
| Runtime and memory | Wall seconds and peak resident memory, with hardware, OS, cache state, and repetitions |
| Reproducibility | Output hash equality across explicitly equivalent runs |

Do not count individual source files or tool components as third-party packages. Report denominators, unresolved identities, false positives, false negatives, and excluded cases. Do not silently discard failed runs or treat component count as accuracy.

Publish one result directory per case and generator version, containing `environment.json`, `command.txt`, `measurements.csv`, `ground-truth.json`, raw outputs, diagnostics, and a review explaining limitations. Ground-truth and measurement schemas can be established with the first reviewed benchmark submission.
