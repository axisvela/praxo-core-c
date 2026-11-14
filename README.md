# PRAXO-CORE for C

C11 implementation of the PRAXO-CORE Core contract with source version `0.9.0`. The normative contract is [`spec/`](spec/README.md); Go remains the reference implementation.

## At a glance

| Field | Value |
| --- | --- |
| Package | `praxo-core-c` |
| Registry | Source / CMake |
| Build | CMake source build (see README) |
| Source version | `0.9.0` |
| Published version | not published |
| Source tag | `c/v0.9.0` |
| Tier | Core |
| Contract | `SPEC_VERSION` `0.2.0` |
| Documentation | https://axisvela.github.io/praxo-core/languages/c/ |
| License | MIT |

## Highlights

- OpenAI-compatible model: native (transport seam)
- Anthropic model: native (transport seam)
- Gemini model: native (transport seam)
- MCP client: native (transport seam)
- Harmovela sink: native (transport seam)
- OpenTelemetry sink: native (transport seam)
- Subagent delegation: native (synchronous seam)
- Retriever: native

## Quick start

This implementation is source-only. Follow the build instructions in [`language/c/README.md`](language/c/README.md).

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native (transport seam) | `PxOpenAICompatible`; caller supplies HTTP transport |
| Anthropic model | native (transport seam) | `PxAnthropic`; caller supplies HTTP transport |
| Gemini model | native (transport seam) | `PxGemini`; caller supplies HTTP transport |
| MCP client | native (transport seam) | `PxMcpClient`; caller supplies `PxMcpTransport` |
| Harmovela sink | native (transport seam) | `praxo_harmovela`; caller supplies HTTP transport |
| OpenTelemetry sink | native (transport seam) | `PxOtelSink`; caller supplies `PxOtelTransport` |
| Subagent delegation | native (synchronous seam) | `px_subagent_run`; no asynchronous manager |
| Retriever | native | `PxDocument`, `PxRetriever`, `px_retrieve` |

## Examples

Runnable examples live under [`language/c/examples`](language/c/examples).

| Example | What it shows |
| --- | --- |
| [checkpoint](language/c/examples/checkpoint) | This example uses the C Core checkpoint allowlist to encode and decode only registered payload types. |
| [event-sink](language/c/examples/event-sink) | This example uses the C Core sink composition to fan out lifecycle and tool events and filter the tool-only stream. |
| [hitl](language/c/examples/hitl) | This example demonstrates a write tool that requires human approval: |
| [identity-policy](language/c/examples/identity-policy) | This example binds a trusted principal to a C Core policy callback and rejects missing, inactive, role-mismatched, and tenant-mismatched actions. |
| [mcp](language/c/examples/mcp) | This example uses a caller-owned in-process transport with the C MCP client. It covers initialize, `tools/list`, and `tools/call` without a server process. |
| [provider-fallback](language/c/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary error when both fail. |
| [retry](language/c/examples/retry) | This example retries a transient failure with a bounded attempt count and preserves the final error when attempts are exhausted. |
| [service](language/c/examples/service) | This example defines a transport-neutral request handler boundary with health, principal, and run cases. Wire it into any C HTTP server. |
| [session-checkpoint](language/c/examples/session-checkpoint) | This example saves and restores a conversation history across two agent turns. It uses the Core allowlist for payload encoding and a teaching in-memory payload. |
| [streaming](language/c/examples/streaming) | This example forwards model deltas through the C Core `on_delta` callback and checks that the deltas reconstruct the final output. |
| [structured-output](language/c/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Verify

Run the checks from `language/c`:

```bash
cd language/c
cmake -S . -B build
cmake --build build
ctest --test-dir build --output-on-failure
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/c/README.md`](language/c/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>

## Repository layout

- `language/c/` — implementation source, tests, API snapshot, and examples
- `spec/` — shared contract, vectors, and parity inventories
- `LICENSE` — MIT license

## Canonical source

- Canonical source: https://github.com/axisvela/praxo-core/tree/main/language/c
- Registry introduction: `language/c/REGISTRY.md`
- Machine-readable entry: `language/c/llms.txt` and `language/c/llms.md`
- Mirror repository: https://github.com/axisvela/praxo-core-c
- Release index: https://axisvela.github.io/praxo-core/languages/registry-status/

This repository is a discovery mirror of the canonical C source. The monorepo remains the source of truth and the release workflow source.

PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

MIT licensed.
