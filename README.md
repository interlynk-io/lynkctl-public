# lynkctl — embedded firmware SBOM generator

Generate CycloneDX SBOMs from C/C++ build evidence and embedded firmware project metadata with Interlynk's lynkctl.

**lynkctl is proprietary software.** This public repository contains documentation, example SBOMs, CI templates, and a place for reproducible benchmarks. The implementation and binary distribution are managed separately.

## Get started

[Contact Interlynk](mailto:support@interlynk.io) for binary access and licensing. With an approved binary installed:

```sh
lynkctl version --json
lynkctl generate ./firmware --evidence -o firmware.cdx.json
```

Data goes to stdout or the output file; diagnostics go to stderr. Add `--strict` to fail on warnings in CI.

## Build evidence for firmware

| Build system | Input |
| --- | --- |
| GNU Make | Makefiles and dry-run compile/link commands |
| CMake | Configured build tree and CMake File API replies |
| IAR Embedded Workbench for Arm | `.ewp` / `.eww` project metadata and configuration |
| TI Code Composer Studio | `.project` / `.cproject` metadata and selected configuration |

Use source files, compiler settings, vendored dependencies, and available linker evidence to explain component identity. A metadata-only run does not prove which bytes shipped; provide matching build artifacts and linker maps when evaluating shipped firmware.

The examples use **lynkctl v0.3.6 and CycloneDX 1.6 JSON**. SPDX license identifiers can appear within CycloneDX documents; this repository does not claim SPDX document output support.

## Documentation

- [Installation and access](docs/installation.md)
- [Firmware generation guide](docs/usage.md)
- [Diagnostics and reproducibility](docs/diagnostics.md)
- [CI integration examples](examples/ci/README.md)
- [Public firmware SBOMs and reproduction instructions](examples/sboms/README.md)
- [Benchmark methodology](benchmark/README.md)
- [Interlynk platform documentation](https://docs.interlynk.io/)
- [CycloneDX specification](https://cyclonedx.org/specification/overview/)

## Inspect real output

| Public firmware example | SBOM | Components | Interpretation |
| --- | --- | ---: | --- |
| FreeRTOS STM32F103 IAR demo | [CycloneDX JSON](examples/sboms/freertos-stm32f103.cdx.json) | 35 | Kernel, source files, and build tools; device identified only as Generic Arm Core |
| FreeRTOS STM32L152 Discovery IAR demo | [CycloneDX JSON](examples/sboms/freertos-stm32l152.cdx.json) | 37 | Kernel, source files, build tools, and STM32L152xB target |

Both examples include pinned upstream revisions, exact commands, output hashes, and diagnostics. Component counts include source files and excluded build tools; they are not counts of third-party packages or an accuracy score.

## Questions and contributions

Use [issues](https://github.com/interlynk-io/lynkctl-public/issues) for public documentation questions and reproducible examples. Send private projects and licensing requests to [support@interlynk.io](mailto:support@interlynk.io). See [contribution guidance](CONTRIBUTING.md) and [rights and attribution](NOTICE.md).
