# Diagnostics and reproducibility

SBOM data goes to stdout or `--output`; diagnostics go to stderr. `-v` shows individual diagnostics, `-vv` adds provenance detail, and `-vvv` adds trace timing. `--quiet` suppresses the summary, not errors.

| Exit code | Meaning |
| --- | --- |
| 0 | No errors; without strict mode, warnings may remain |
| 1 | Errors, or warnings promoted by `--strict` |
| 2 | Invalid usage or conflicting options |

Preserve stderr and the exit code with every evaluation. A valid CycloneDX document can still contain incomplete component metadata. Schema validity, completeness, and correct identification are separate checks.

```sh
lynkctl generate ./firmware --evidence --reproducible \
  --timestamp 2026-09-19T00:00:00Z \
  -o firmware.cdx.json 2>firmware.diagnostics.txt
```

For stable comparisons, pin the source and submodules, generator version, selected target/configuration, timestamp, toolchain, enrichment database, and build artifacts. Absolute evidence paths may affect output across checkout locations: our byte-identity check repeats the command in the same checkout. It is not a claim of path-independent reproducibility.

The public examples disable OSS-index matching and OS package lookup so results do not depend on a locally cached index or host package database. This reduces available enrichment; evaluate full enrichment separately. Their explicit timestamp is a reproduction parameter, not a firmware build date.
