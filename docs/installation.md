# Installation and access

Request a lynkctl binary and applicable license from [support@interlynk.io](mailto:support@interlynk.io). This repository does not distribute the implementation or binaries. Use the download location and checksum supplied by Interlynk; a public installer is not assumed here.

Place the approved executable on `PATH`, then verify:

```sh
lynkctl version --json
lynkctl generate --help
```

Examples here were exercised with v0.3.6 on Linux amd64. Record your binary version and checksum when comparing results. Provision the same approved version on your CI runner.

GNU Make analysis requires GNU Make and whatever tools the project's metadata evaluation needs. CMake analysis requires an already configured build tree with File API replies. IAR metadata parsing does not require an installed IAR compiler. Building firmware separately may require vendor tools and licenses.

The [usage guide](usage.md) covers provider selection; the [CI examples](../examples/ci/README.md) assume an already provisioned runner.
