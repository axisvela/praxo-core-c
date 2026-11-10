# PRAXO-CORE for C

Dedicated repository for the C implementation of PRAXO-CORE: an
embeddable, MIT-licensed agent execution kernel with policy controls,
human-in-the-loop approval, checkpoints, events, and tool calling.

- Package: `praxo-core-c` (`0.6.0`)
- Registry: source / CMake
- Documentation: https://axisvela.github.io/praxo-core/languages/c/
- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/c
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical C source. The
monorepo remains the source of truth and the release workflow source. Shared
conformance vectors are included under `spec/`.

## Install or build

Source build with CMake from `language/c`.

## Verify

Build and test instructions are in `language/c/README.md`. The
monorepo CI runs the language's conformance, API snapshot, and native tests.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety
controller. Do not infer exactly-once execution, complete sandbox isolation,
production security certification, live-provider behavior, or physical safety
from this package.

MIT licensed.