Create a reusable Claude Code command in this project called **WaitGo**.

Goal: install a command that lets the user send several instructions in a row, while Claude Code waits until the user writes exactly `go` before starting any work.

To do:

1. Before creating anything, ask me where to install the command:

   * **Global (recommended)**: `~/.claude/commands/wait-go.md`, available in all my Claude Code sessions.
   * **Project only**: `.claude/commands/wait-go.md`, versioned with this repository and shared with my team.

   Wait for my answer before continuing. If I pick the global install, tell me that writing outside the project may trigger a permission prompt.

2. Create the target folder if it does not already exist.
3. Create the command file at the location I chose.
4. Put exactly the following command content inside the file:

```md
You will receive several instructions in a row.

Mandatory rule: do not start any action, file modification, detailed analysis, or execution plan until I send a message whose entire content is exactly the three lowercase characters: go

Global rule:

* reply in the user's language.

Before go:

* treat every message I send as another queued instruction;
* do not accept `Go`, `GO`, quoted `"go"`, `go` followed by punctuation, or a message containing any other text as the trigger;
* reply only with: `Instruction received. Send me another instruction or write "go" if you want me to start processing the instructions.`
* do not add greetings, explanations, formatting, or status details to that acknowledgement;
* remember the instructions;
* do not start any task;
* do not propose an execution plan yet;

When I write exactly `go`:

* reread all received instructions;
* group them into coherent blocks;
* identify dependencies, duplicates, ambiguities, or possible conflicts;
* propose a clear execution order;
* process the tasks step by step, block by block;
* after each block, summarize what was done before moving to the next one;
* only ask for validation if there is a conflict, a major risk, or a blocking ambiguity;
* otherwise, make reasonable assumptions and continue;

At the end:

* provide a very concise summary of what was done;
* indicate the execution order followed;
* list the files created or modified;
* mention any important assumption, limitation, or unresolved point;

Do not modify anything else in the project.
```

Constraints:

* Do not modify any other file.
* Do not rename existing commands.
* Do not add dependencies.
* Do not change project configuration.
* Keep the command file simple and readable.

At the end, simply tell me:

* the file created and whether the install is global or project-scoped;
* how to use the command in Claude Code, for example: `/wait-go`.
