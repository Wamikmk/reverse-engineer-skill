# Image-to-skill conversion plan

## Goal and deliverables

Convert the supplied research-note prompt into a globally discoverable Codex skill named `reverse-engineer`, installed in the user-level `.codex/skills/reverse-engineer` folder.

1. Inspect the original-resolution image and transcribe all visible text, including UI, header, prompt, and footer, into `image-transcription.md`.
2. Convert the prompt's placeholders into task intake and conditional workflow instructions in `../SKILL.md`.
3. Preserve the evidence model, engine check, guided-prompt routing, unknown tracking, behavioral specification, specification-mediated implementation, and negative-control verification.
4. Add `../agents/openai.yaml` for the display name, short description, and `$reverse-engineer` invocation example. Leave automatic discovery enabled by default.
5. Run the bundled skill validator, check metadata and local reference links, and review instruction boundaries. REA execution is outside this creation task.

## Adaptation decisions

| Image instruction | Reusable skill treatment |
| --- | --- |
| Claude Code / Opus 5.5 branding | Preserve in the transcription; avoid tying the workflow to a specific assistant/model. |
| REA 6.5.0 engine and prompt claims | Preserve as source claims; discover actual MCP schemas and check the installed release's documentation before analysis. |
| Everything runs locally and nothing leaves the machine | Require local REA analysis and no external target-file uploads; distinguish that from an unverified claim that the entire assistant platform is offline. |
| Labels on every line | Require labels on substantive findings; plans, setup statements, and questions remain distinguishable from evidence. |
| Missing engine: one command and stop | Give a documented platform-specific command when verified, otherwise report the missing information; stop dependent analysis without silently installing or substituting engines. |
| No source, strings, or constants lifted | Preserve the restriction on copying internals; allow evidence-backed externally observable values and measured behavior in the spec. |
| SPEC.md from observed behavior alone | Separate supported behavior, inferences, and unresolved requirements; do not promote static evidence into unobserved runtime facts. |
| Always build under ./my-version | Build only when reconstruction is requested; retain the directory as a default in the project workspace. |
| Wait for my go before analysis | Honor this checkpoint when explicitly requested; preserve existing authorization rather than requiring repeated approval for every invocation. |
| Never rerun a retained analysis | Reuse evidence by default; allow reruns when changed inputs, missing evidence, or independent verification justify them. |
| record_unknown | Discover the installed tool and schema; keep a disclosed local register if persistent recording is unavailable. |
| Test the tests with a wrong answer | Require a known-wrong negative control and keep it isolated from the final passing verification. |

## Validation boundary

The transcription is checked against the supplied image. Skill validation establishes packaging and instruction consistency; it does not establish the image's REA/version claims or prove runtime integration. Installing REA, configuring MCP, purchasing engines, and analyzing a target are separate tasks requiring a concrete target and the applicable authorization.
