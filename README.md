# PRAXO-CORE for C

Dedicated repository for the C implementation of PRAXO-CORE: an
embeddable, MIT-licensed agent execution kernel with policy controls,
human-in-the-loop approval, checkpoints, events, and tool calling.

- Package: `praxo-core-c` (`0.6.0`)
- Registry: Source / CMake
- Install: `CMake source build (see README)`
- Documentation: https://axisvela.github.io/praxo-core/languages/c/
- Examples: https://github.com/axisvela/praxo-core-c/tree/main/language/c/examples
- Mirror repository: https://github.com/axisvela/praxo-core-c
- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/c
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical C source.
The monorepo remains the source of truth and the release workflow source. Shared
conformance vectors are included under `spec/`, so the implementation can be
built and tested here.

## Verify

Build and test instructions are in `language/c/README.md`. The
monorepo CI runs the language's conformance, API snapshot, and native tests.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety
controller. Do not infer exactly-once execution, complete sandbox isolation,
production security certification, live-provider behavior, or physical safety
from this package.

MIT licensed.
