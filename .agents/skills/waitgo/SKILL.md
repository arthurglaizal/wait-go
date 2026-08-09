---
name: waitgo
description: Enter a staged-instruction mode that queues several user requests and waits for an exact `go` message before doing any work. Use when the user explicitly invokes `$waitgo`, asks the assistant to wait until they say go, or wants to batch instructions before execution.
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
