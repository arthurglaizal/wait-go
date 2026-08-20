Install **WaitGo** in Claude Code.

Goal: WaitGo lets me send several instructions in a row while Claude Code queues them, and starts working only when I send a message whose entire content is exactly `go`.

**Important:** do not trust any folder, file path, or format taken from memory, from older tutorials, or from this prompt. Claude Code changes its formats and locations over time. Work out what is current **now**, at the moment you run this.

## 1. Ask me first, then wait

Ask me where to install WaitGo:

* **Personal / global (recommended)**: available in all my Claude Code sessions, in every project. WaitGo is a way of working, not project content.
* **Project only**: stored inside this repository, versioned, shared with my team.

Wait for my answer before creating, moving, or writing anything.

## 2. Find out what Claude Code supports today

Before resolving any path:

* Read Claude Code's current official documentation about reusable, user-invocable instruction files (skills, custom commands, or whatever the product calls them today). Start from the official Claude Code documentation site and follow any redirect you hit — the documentation has moved before.
* From that documentation, identify the format the product currently documents as the recommended one for this kind of reusable instruction, and the location matching the scope I chose.
* Then look at my machine: the installed Claude Code version, which of the documented folders already exist, and whether an older format is already in use here.
* If the documentation and my local environment disagree, tell me and ask which one to follow.

Do not assume the answer is the same as last year, or the same as what this repository already contains.

## 3. Show me the resolved path before writing

Print:

* the format you selected and why it is the current recommended one;
* the exact absolute path you are about to create;
* the exact name I will type to invoke WaitGo.

If the target is outside this project, tell me clearly that writing there may require my approval or a permission prompt, and let me approve it.

## 4. Check for an existing installation

Before writing, check whether WaitGo is already installed at the resolved location **or** in any other location the current documentation still recognises, including an older format.

Treat these as existing installations:

* a real folder or file;
* a symlink pointing to a valid target, for example a local clone of the WaitGo repository;
* a **broken** symlink whose target no longer exists — report it as broken and ask me what to do.

If something already exists, never overwrite it silently. Show me the differences between what is there and what you would write, then ask me to confirm.

## 5. Create the files

Create only what the current format actually requires: the instruction file itself, plus any metadata or folder structure the product requires today.

The name I type to invoke WaitGo must be **`wait-go`**. Put that name wherever the current format expects it — folder name, file name, or a metadata field. Check the documentation instead of guessing.

Do not create any legacy or deprecated format by default. If a legacy format is still supported and I explicitly ask for it, you may add it afterwards, clearly presented as optional and secondary.

The behaviour below must be preserved **exactly**. Copy this text as the instruction content. You may only adapt the wrapping — add the metadata block or frontmatter fields the current format requires — never the rules themselves:

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

If the current format requires a description or a similar field, use this one:

```txt
Queue several instructions in a row and start working only when the user sends a message whose entire content is exactly `go`. Use when the user invokes it directly or asks you to wait until they say go.
```

## 6. Validate

After writing:

* confirm the file exists at the path you announced;
* confirm it is valid for the current format, for example that any required metadata is present and well-formed;
* if Claude Code offers a way to list or check installed skills or commands, use it and show me the result.

## 7. Tell me

Keep it short:

* what was created, where, and whether the install is personal/global or project-scoped;
* how to invoke WaitGo, and how to use it: send instructions one by one, then write exactly `go`;
* whether a restart or a new conversation is needed before it is detected;
* anything you could not confirm in the official documentation.

## Constraints

* Do not modify any other file in this project.
* Do not rename or delete existing skills, commands, or prompts.
* Do not add dependencies.
* Do not change project configuration.
* Keep the installed file simple and readable.
