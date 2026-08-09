Create a reusable AI assistant command, instruction file, skill, or equivalent setup in this project called **WaitGo**.

Goal: install a reusable mode that lets the user send several instructions in a row, while the AI assistant waits until the user writes exactly `go` before starting any work.

First, inspect the project structure and determine the best supported location and format for this kind of reusable instruction in the current AI coding environment.

Then, if the current environment also supports a user-level location (available in every project, usually under the home directory), ask me where to install it:

* **Global (recommended)**: available in all my sessions, since WaitGo is a way of working rather than project-specific content.
* **Project only**: versioned with this repository and shared with my team.

Wait for my answer before creating anything, and warn me if writing outside the project requires an approval or is blocked by a sandbox. If the environment supports only a project-level location, skip the question, install in the project, and tell me why.

Examples:

* a command file;
* a reusable prompt file;
* an instruction file;
* a skill file;
* a documented prompt in the project docs;
* any equivalent mechanism supported by the current AI tool.

Use the simplest and most native option for the current environment.

The reusable instruction must enforce this behavior:

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

* Do not modify unrelated files.
* Do not add dependencies.
* Do not change project configuration unless it is strictly required for this AI environment to recognize the reusable instruction.
* Keep the setup simple and readable.
* Prefer a native command or instruction mechanism if the current AI coding tool supports one.
* If no native mechanism exists, create a clear Markdown prompt file in a relevant docs or prompts folder.

At the end, simply tell me:

* what file or instruction was created;
* where it was created, and whether the install is global or project-scoped;
* how to use WaitGo with the current AI assistant;
* any limitation if the current tool does not support reusable commands directly.
