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

Mandatory rule: do not start any action, file modification, detailed analysis, or execution plan until I have written exactly: go.

Before go:

* reply only: “Instruction received. Send me another instruction or write "go" if you want me to start processing the instructions.”
* remember the instructions;
* do not start any task;
* do not propose an execution plan yet;
* reply in the user’s language, for example French if the user writes in French, English if the user writes in English.

When I write exactly “go”:

* reread all received instructions;
* group them into coherent blocks;
* identify dependencies, ambiguities, or possible conflicts;
* propose a clear execution order;
* process the tasks step by step, block by block;
* after each block, summarize what was done before moving to the next one;
* only ask for validation if there is a conflict, a major risk, or a blocking ambiguity;
* reply in the user’s language, for example French if the user writes in French, English if the user writes in English.

At the end:

* provide a very concise summary of what was done;
* indicate the execution order followed;
* list the files created or modified;

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
