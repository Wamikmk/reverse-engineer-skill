# Reverse Engineer Anything

I turned a reverse-engineering prompt from an image into a reusable Codex skill. The goal is to understand how a software feature works and keep the evidence behind each claim.

The repo includes the skill, the full image transcription, the conversion decisions, and a beginner guide.

## What it does

1. **Check the setup.** Identify the target and verify the REA MCP connection and required analysis engine. Stop dependent analysis if a required tool is missing.
2. **Trace the feature.** Map the app, then follow the relevant modules and functions. Explain what each tool call should answer.
3. **Separate findings.** Mark direct evidence as an observation, an interpretation as an inference, and an unanswered question as an unknown. Keep unknowns visible.
4. **Write the behavior down.** Produce `SPEC.md` when requested, with inputs, outputs, boundaries, errors, and measured examples. Mark anything the evidence does not establish.
5. **Build only when requested.** Write an independent implementation from the specification. Test recorded behavior and confirm the comparison rejects a deliberately wrong result.

The report ends with what is proven, what is inferred, what is still unknown, and which checks could resolve the gaps.

## What you need

1. **Codex with the skill installed.** The skill is an instruction file that guides the assistant.
2. **REA connected through MCP.** REA provides the analysis tools. MCP lets the assistant call them.
3. **The engine your target requires.** Check the installed REA release's documentation. Requirements depend on the target and release.
4. **A target you may examine.** Provide a specific feature and the actions you authorize.

Installing this skill does not install REA or configure its MCP connection.

## Install

Download or clone this repo. Copy the `reverse-engineer` folder into your global Codex skills folder.

For the default Windows location, run this from the repo root:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.codex\skills" | Out-Null
Copy-Item -LiteralPath .\reverse-engineer -Destination "$env:USERPROFILE\.codex\skills" -Recurse
```

For the default macOS or Linux location:

```bash
mkdir -p ~/.codex/skills
cp -R reverse-engineer ~/.codex/skills/
```

If you use a custom `CODEX_HOME`, use its `skills` folder. If `reverse-engineer` is already installed, inspect the existing version before replacing it.

## Use

Invoke the skill in a Codex session where it is available:

```text
Use $reverse-engineer.

Target: [absolute path or URL]
Question: How does [specific feature] work?
Scope: [why I may examine this target]
Permission: Static inspection only. Do not launch or interact with the target.
Output: Explain the evidence and write SPEC.md.
Checkpoint: Show the plan and wait for my go.
```

If you want a replacement, add your language and output directory:

```text
Build an independent Python version from SPEC.md under ./my-version.
Test the recorded behavior. Keep unresolved requirements visible.
```

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](reverse-engineer/SKILL.md) | The investigation workflow. |
| [openai.yaml](reverse-engineer/agents/openai.yaml) | Display metadata and invocation example. |
| [Image transcription](reverse-engineer/references/image-transcription.md) | All visible text from the original image. |
| [Conversion plan](reverse-engineer/references/conversion-plan.md) | What changed when the prompt became a skill and why. |
| [Beginner guide](reverse-engineer-beginner-guide.html) | A standalone explanation with a worked example and first request. Download it and open it in a browser. |

## Boundaries

1. **Keep execution explicit.** Static inspection is the default. Running, attaching to, or interacting with the target needs authorization covering that action.
2. **Keep claims tied to evidence.** A missing result in an incomplete search does not prove a behavior is absent.
3. **Reconstruct from behavior.** Keep copied source and internal implementation details out of the replacement.
4. **Check privacy requirements.** Local REA analysis does not establish that the whole assistant system is offline. Verify any requirement that nothing leave the machine.

## Validation and source

The bundled skill validator passed. Reference links and invocation metadata were checked. The guide preserves the typesetter template CSS and contains no JavaScript or external resources.

A live REA investigation has not been tested.

The source image credits the prompt to **@zodchiii** and REA to **morluto/rea**. Its version and engine claims are preserved in the transcription and have not been independently verified. The skill checks the installed release's documentation before analysis.
