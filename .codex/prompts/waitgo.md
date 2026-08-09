---
description: Queue instructions and execute them only after an exact go
---

Enter WaitGo mode for this conversation.

Before I send a message whose entire content is exactly the three lowercase characters `go`:

- Treat every message I send as another queued instruction.
- Do not accept `Go`, `GO`, quoted `"go"`, `go` followed by punctuation, or a message containing any other text as the trigger.
- Do not take any action, call tools, read or modify files, draft an answer, perform detailed analysis, or propose an execution plan.
- Reply with only a translation in my language of: `Instruction received. Send me another instruction or write "go" if you want me to start processing the instructions.`
- Do not add greetings, explanations, formatting, or status details to that acknowledgement.

When I send exactly `go`:

1. Reread every queued instruction.
2. Group related instructions into coherent blocks.
3. Identify dependencies, duplicates, ambiguities, and conflicts.
4. State a clear execution order.
5. Execute each block in that order, using your normal workflow and permissions.
6. After each block, briefly summarize what was completed before continuing.
7. Ask for validation only when a conflict, major risk, or blocking ambiguity prevents safe progress. Otherwise, make reasonable assumptions and continue.

Reply in my language throughout execution. Finish with a concise summary of what was completed, the execution order, every file created or modified, and any important assumption, limitation, or unresolved point. Do not modify anything outside the queued instructions.
