Create a reusable Codex skill called **WaitGo**.

Goal: install a skill that lets the user send several instructions in a row, while Codex waits until the user writes exactly `go` before starting any work.

To do:

1. Create the `.agents/skills/waitgo/agents/` folder if it does not already exist.
2. Create this file: `.agents/skills/waitgo/SKILL.md`
3. Put exactly the following content inside the file:

````md
---
name: waitgo
description: Enter a staged-instruction mode that queues several user requests and waits for an exact `go` message before doing any work. Use when the user explicitly invokes `$waitgo`, asks Codex to wait until they say go, or wants to batch instructions before execution.
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
5. Execute each block in that order, using the normal Codex workflow and permissions.
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

4. Create this file: `.agents/skills/waitgo/agents/openai.yaml`
5. Put exactly the following content inside the file:

```yaml
interface:
  display_name: "WaitGo"
  short_description: "Batch instructions until you say go."
  default_prompt: "Use $waitgo to queue my next instructions until I say exactly \"go\"."
policy:
  allow_implicit_invocation: false
```

Optional legacy compatibility:

If the user also wants the deprecated custom-prompt mechanism, create `.codex/prompts/waitgo.md` with the same behavior, using this front matter and rewriting the rules in the first person:

```md
---
description: Queue instructions and execute them only after an exact go
---
```

Constraints:

* Do not modify any other file.
* Do not rename existing skills or prompts.
* Do not add dependencies.
* Do not change project configuration.
* Keep the skill files simple and readable.

At the end, simply tell me:

* the files created;
* how to invoke the skill in Codex, for example: `$waitgo`;
* that a new chat or a Codex restart may be needed for the skill to be detected;
* that Codex reserves root slash commands, so there is no custom `/waitgo` alias, and the deprecated prompt form would be `/prompts:waitgo`.
