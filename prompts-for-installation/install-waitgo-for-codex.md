Install **WaitGo** in Codex.

Goal: WaitGo lets me send several instructions in a row while Codex queues them, and starts working only when I send a message whose entire content is exactly `go`.

**Important:** do not trust any folder, file path, or format taken from memory, from older tutorials, or from this prompt. Codex changes its formats and locations over time. Work out what is current **now**, at the moment you run this.

## 1. Ask me first, then wait

Ask me where to install WaitGo:

* **Personal / global (recommended)**: available in all my Codex sessions, in every project. WaitGo is a way of working, not project content.
* **Project only**: stored inside this repository, versioned, shared with my team.

Wait for my answer before creating, moving, or writing anything.

## 2. Find out what Codex supports today

Before resolving any path:

* Read Codex's current official documentation about reusable, invocable instruction sets (skills, custom prompts, or whatever the product calls them today). Start from the official Codex documentation site and follow any redirect you hit — the documentation has moved before.
* From that documentation, identify the format the product currently documents as the recommended one for this kind of reusable instruction, which files and metadata it requires, and the location matching the scope I chose.
* Then look at my machine: the installed Codex version, which of the documented folders already exist, and whether an older format is already in use here.
* If the documentation and my local environment disagree, tell me and ask which one to follow.

Do not assume the answer is the same as last year, or the same as what this repository already contains.

## 3. Show me the resolved path before writing

Print:

* the format you selected and why it is the current recommended one;
* the exact absolute path you are about to create, and every file you will put in it;
* the exact form I will type to invoke WaitGo.

If the target is outside this workspace, tell me clearly that the default sandbox may block writing there and that it will require my approval, and let me approve it.

## 4. Check for an existing installation

Before writing, check whether WaitGo is already installed at the resolved location **or** in any other location the current documentation still recognises, including an older or deprecated one.

Treat these as existing installations:

* a real folder or file;
* a symlink pointing to a valid target, for example a local clone of the WaitGo repository — in that case tell me it is already installed and stop;
* a **broken** symlink whose target no longer exists — report it as broken and ask me what to do.

If something already exists, never overwrite it silently. Show me the differences between what is there and what you would write, then ask me to confirm.

## 5. Create the files

Create only what the current format actually requires: the instruction file itself, plus any companion metadata file or folder structure the product requires today. Check the documentation for which fields are required and which are optional, instead of copying an old example.

The name I type to invoke WaitGo must be **`waitgo`**. Put that name wherever the current format expects it — folder name, file name, or a metadata field.

Do not create any legacy or deprecated format by default. If a legacy format is still supported and I explicitly ask for it, you may add it afterwards, clearly presented as optional and secondary.

The behaviour below must be preserved **exactly**. Copy this text as the instruction content. You may only adapt the wrapping — add, rename, or drop metadata fields so the file matches what the current format requires — never the rules themselves:

````md
---
name: waitgo
description: Enter a staged-instruction mode that queues several user requests and waits for an exact `go` message before doing any work. Use when the user explicitly invokes the skill, asks the assistant to wait until they say go, or wants to batch instructions before execution.
---

# WaitGo

Enter WaitGo mode for the current conversation. Keep all queued instructions in the conversation context until the user triggers execution.

## Before `go`

- Treat every subsequent user message as another queued instruction unless its entire content is exactly the three lowercase characters `go`.
- Do not accept `Go`, `GO`, quoted `"go"`, `go` followed by punctuation, or a message containing any other text as the trigger.
- Do not take any action, call tools, read or modify files, draft an answer, perform detailed analysis, or propose an execution plan.
- Reply with only a translation in the user's language of: `Instruction received. Send me another instruction or write "go" if you want me to start processing the instructions.`
- Do not add greetings, explanations, formatting, or status details to that acknowledgement.

## When the user sends exactly `go`

1. Reread every instruction queued since WaitGo mode started.
2. Group related instructions into coherent blocks.
3. Identify dependencies, duplicates, ambiguities, and conflicts.
4. State a clear execution order.
5. Execute each block in that order, using your normal workflow and permissions.
6. After each block, briefly summarize what was completed before continuing.
7. Ask for validation only when a conflict, major risk, or blocking ambiguity prevents safe progress. Otherwise, make reasonable assumptions and continue.

Reply in the user's language throughout execution.

## Completion

Finish with a concise summary that includes:

- what was completed;
- the execution order followed;
- every file created or modified;
- any important assumption, limitation, or unresolved point.

Do not modify anything outside the queued instructions.
````

If the current format supports an optional companion file for how the skill is presented and invoked, and the documentation still describes those fields, use this content and adapt the field names to what is documented today. WaitGo must never be triggered implicitly — only when I invoke it myself:

```yaml
interface:
  display_name: "WaitGo"
  short_description: "Batch instructions until you say go."
  default_prompt: "Queue my next instructions with WaitGo until I say exactly \"go\"."
policy:
  allow_implicit_invocation: false
```

If the field that disables implicit invocation no longer exists or has been renamed, tell me instead of silently dropping the intent.

## 6. Validate

After writing:

* confirm every file exists at the paths you announced;
* confirm they are valid for the current format, for example that required metadata is present and the YAML parses;
* if Codex offers a way to list installed skills or prompts, use it and show me the result.

## 7. Tell me

Keep it short:

* what was created, where, and whether the install is personal/global or project-scoped;
* how to invoke WaitGo, and how to use it: send instructions one by one, then write exactly `go`;
* whether a restart or a new conversation is needed before it is detected;
* anything you could not confirm in the official documentation.

## Constraints

* Do not modify any other file in this project.
* Do not rename or delete existing skills or prompts.
* Do not add dependencies.
* Do not change project configuration.
* Keep the installed files simple and readable.
