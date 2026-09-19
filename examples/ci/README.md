# CI integration examples

Copy [github-actions.yml](github-actions.yml) into your firmware repository's `.github/workflows/`, or adapt [gitlab-ci.yml](gitlab-ci.yml) for GitLab. Both are opt-in examples for a trusted, pre-provisioned runner with an approved lynkctl binary, firmware toolchain, dependencies, and any required license. They do not download proprietary binaries.

The examples use GNU Make with `--strict`, a commit-derived timestamp, captured diagnostics, and retained artifacts even on generation failure. Change the provider and configuration to match your project using the [usage guide](../../docs/usage.md). Projects with metadata warnings will fail until those warnings are resolved; artifact retention does not indicate success.

The GitHub example is manually dispatched and expects labels `self-hosted`, `linux`, and `lynkctl`. The GitLab example uses a manually started web pipeline and a runner tagged `lynkctl`. Run only trusted code on these runners. These integration templates have not been executed against a user's firmware runner.
