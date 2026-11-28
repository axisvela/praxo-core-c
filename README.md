# PRAXO-CORE for C

PRAXO-CORE (also written praxocore) is an embeddable, MIT-licensed agent framework. C11 implementation of the PRAXO-CORE Core contract with source version `0.12.0`. The normative contract is [`spec/`](https://github.com/axisvela/praxo-core/blob/main/spec/README.md); Go remains the reference implementation.

## At a glance

| Field | Value |
| --- | --- |
| Package | `praxo-core-c` |
| Registry | [xmake](https://packages.xmake.io/packages/praxo-core) |
| Install | `xrepo install praxo-core` |
| Source version | `0.14.0` |
| Published version | `0.13.0` |
| Publication status | published on xmake 0.13.0 (source 0.14.0); vcpkg and Conan submissions open |
| Canonical source tag | [`c/v0.14.0`](https://github.com/axisvela/praxo-core/tree/c/v0.14.0) |
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

Install the published package:

```text
xrepo install praxo-core
```

See the [full C README](language/c/README.md) for complete installation, build, and verification commands.

## What's included

| Capability | Status | Detail |
| --- | --- | --- |
| OpenAI-compatible model | native (transport seam) | `PxOpenAICompatible`; caller supplies HTTP transport; `px_openai_generate_stream` reassembles SSE content, tool calls, usage, and finish reason |
| Anthropic model | native (transport seam) | `PxAnthropic`; caller supplies HTTP transport; `px_anthropic_generate_stream` reassembles Anthropic SSE |
| Gemini model | native (transport seam) | `PxGemini`; caller supplies HTTP transport; `px_gemini_generate_stream` reassembles Gemini SSE |
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
| [consumer](language/c/examples/consumer) | This example runs a deterministic model against the C Core, registers one `record(target)` tool, applies an explicit tool scope plus policy, and checks that an allowed call produces one effect while a denied call produces none. |
| [event-sink](language/c/examples/event-sink) | This example uses the C Core sink composition to fan out lifecycle and tool events and filter the tool-only stream. |
| [hitl](language/c/examples/hitl) | This example demonstrates a write tool that requires human approval: |
| [identity-policy](language/c/examples/identity-policy) | This example binds a trusted principal to a C Core policy callback and rejects missing, inactive, role-mismatched, and tenant-mismatched actions. |
| [live-model](language/c/examples/live-model) | This example connects the C Core to an OpenAI-compatible endpoint through the existing `px_openai_generate` adapter and registers one low-risk `get_time(zone)` tool. The model may only call `get_time`; every other tool call is denied by policy. |
| [mcp](language/c/examples/mcp) | This example uses a caller-owned in-process transport with the C MCP client. It covers initialize, `tools/list`, and `tools/call` without a server process. |
| [provider-fallback](language/c/examples/provider-fallback) | This example calls a fallback only after the primary fails and preserves the primary error when both fail. |
| [retry](language/c/examples/retry) | This example retries a transient failure with a bounded attempt count and preserves the final error when attempts are exhausted. |
| [service](language/c/examples/service) | This example defines a transport-neutral request handler boundary with health, principal, and run cases. Wire it into any C HTTP server. |
| [session-checkpoint](language/c/examples/session-checkpoint) | This example saves and restores a conversation history across two agent turns. It uses the Core allowlist for payload encoding and a teaching in-memory payload. |
| [streaming](language/c/examples/streaming) | This example forwards model deltas through the C Core `on_delta` callback and checks that the deltas reconstruct the final output. |
| [structured-output](language/c/examples/structured-output) | This example validates a final JSON answer against a schema and rejects invalid output. |

## Scenario Tutorials

Scenario-oriented tutorials live under `language/c/Tutorial`. Planning context: [Tutorial Plan](https://axisvela.github.io/praxo-core/getting-started/tutorial-plan/), [100 candidate agent scenarios](https://axisvela.github.io/praxo-core/getting-started/agent-scenarios/), and [Tutorial Catalog](https://axisvela.github.io/praxo-core/getting-started/tutorial-catalog/).

| Path | What it shows |
| --- | --- |
| [Tutorial](language/c/Tutorial) | Bounded C examples built on the native Core. Each tutorial is a small, runnable slice with explicit non-goals and an application-owned boundary; none is a complete industry product. |
| [aquaculture-water](language/c/Tutorial/aquaculture-water) | Computes fixed oxygen/temperature indicators and drafts a bounded review action. No aerator or feeder command. |
| [device-diagnostics](language/c/Tutorial/device-diagnostics) | A scoped device tutorial over the native MIT C Core. It reads one fixed `device-100` diagnostic snapshot through an application-owned `PxDeviceAdapter` function pointer and drafts an operator review action. The adapter is an in-process fixture. This tutorial does not implement a real serial bus, socket, device SDK, live model or device write. |
| [hvac-settings](language/c/Tutorial/hvac-settings) | Reads fixed building conditions and drafts review-only HVAC/lighting settings. No BMS command or verified energy savings. |
| [lab-loop](language/c/Tutorial/lab-loop) | Simulates one fixed parameter/result cycle and drafts review-only next parameters. No actuator, chemical handling or autonomous experiment. |
| [livestock-monitor](language/c/Tutorial/livestock-monitor) | Summarizes fixed animal observations and drafts a review-only veterinary request. No diagnosis, isolation or feeding control. |
| [npc-narrative](language/c/Tutorial/npc-narrative) | Reads fixed character state and drafts one scoped host action with an observed result. No arbitrary host commands. |
| [world-economy](language/c/Tutorial/world-economy) | Simulates one fixed economy tick and drafts a review-only balance action. No long-term equilibrium or scale guarantee. |

## Reference Applications

No accepted end-to-end reference application is recorded for this language yet. Candidate goals are tracked in the [Reference Application Portfolio](https://axisvela.github.io/praxo-core/project/roadmap/#reference-application-portfolio).

## Verify

Run the checks from `language/c`:

```bash
cd language/c
cmake -S . -B build
cmake --build build
ctest --test-dir build --output-on-failure
```

This mirror contains the language source and the shared `spec/` vectors, so the implementation can be built and tested here. See [`language/c/README.md`](language/c/README.md) for the exact commands. The monorepo CI runs conformance, API snapshot, and native tests for this implementation.

## Boundaries

Reference application source is not end-to-end portfolio acceptance; follow each README's scope and evidence.
PRAXO-CORE is not a hosted model, workflow engine, identity provider, or safety controller. Do not infer exactly-once execution, complete sandbox isolation, production security certification, live-provider behavior, or physical safety from this package.

## Community

- X: <https://x.com/axisvela>
- Weibo: <https://weibo.com/u/1936025761>
- LinkedIn: <https://www.linkedin.com/company/axisvela/>
- Facebook: <https://www.facebook.com/profile.php?id=61596905732406>
- YouTube: <https://www.youtube.com/@axisvela>
- Discord: <https://discord.com/channels/1575163993767809064/1575164343148875977>
- GitHub Discussions: <https://github.com/axisvela/praxo-core/discussions>
- GitHub Issues: <https://github.com/axisvela/praxo-core/issues>
- Documentation: <https://axisvela.github.io/praxo-core/>
- Architect: <https://axisvela.architect.pub>

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

This repository is a discovery mirror of the canonical C source. The monorepo remains the source of truth and the release workflow source. The mirror's `main` branch tracks current source, not a release snapshot. Source tags refer to the canonical monorepo and are not necessarily present in this mirror; syncing the branch does not publish mirror tags or registry packages.


MIT licensed.
