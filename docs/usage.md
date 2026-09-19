# Generate a firmware SBOM

These commands use options exposed by lynkctl v0.3.6. Select the provider explicitly when a tree contains several build systems.

## GNU Make

```sh
lynkctl generate ./firmware --provider gnu-make \
  --make-target all --evidence -o firmware.cdx.json
```

Pass build variables with repeated `--make-config-vars KEY=VALUE`. Make analysis uses dry-run commands; Makefile evaluation and recursive Make can still execute helper commands. Use a trusted project and a controlled runner.

## CMake

Request File API metadata before configuring:

```sh
mkdir -p build/.cmake/api/v1/query
touch build/.cmake/api/v1/query/codemodel-v2
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
lynkctl generate . --provider cmake --cmake-build-dir ./build \
  --evidence -o firmware.cdx.json
```

Add the project's usual toolchain and board configuration arguments to the configure command. Use `--cmake-target NAME` when selecting one firmware target.

## IAR Embedded Workbench for Arm

```sh
lynkctl generate ./firmware.ewp --provider iar --iar-config Release \
  --evidence -o firmware.cdx.json
```

Configuration names must match the project. Use `--iar-all-configs -o ./sboms/` to emit separate files for all configurations.

## TI Code Composer Studio

```sh
lynkctl generate ./firmware --provider ccs --ccs-config Release \
  --evidence -o firmware.cdx.json
```

Keep referenced generated-build metadata and source paths available. Use `--ccs-build-dir` when it is outside the selected configuration directory.

## Explain the result

- `--include-source-files --exclude-header-files`: include source-file components.
- `--evidence`: include supported identity and occurrence evidence.
- `--map-file ./build/firmware.map`: supply a matching linker map explicitly.
- `--distribution-file ./release/firmware.bin`: select the distributed artifact to hash.
- `--no-map`: intentionally omit map and link-info evidence.
- `--no-oss-index`: disable vendored OSS-index matching.
- `--strict`: fail on warnings as well as errors.

Use build outputs from the same configuration and revision as the inspected metadata.
