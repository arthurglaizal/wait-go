<p align="center">
  <img src="./public/waitgo-demo-1500w-24fps.gif" alt="WaitGo demo animation" width="100%" />
</p>

# WaitGo

> **Batch your instructions, then execute only when you say go.**

WaitGo is a minimal Claude Code slash command setup that lets you stage several instructions before execution.

Instead of reacting to each instruction immediately, Claude Code waits until you write `go`, then processes everything as one consolidated sequence.

## Why?

Sometimes you have several corrections, requests, or implementation notes to send, but you do not want Claude Code to start working after the first one.

WaitGo lets you gather your feedback first, trigger execution once with `go`, and let Claude Code work through the full sequence while you focus on something else or just go grab a coffee.

## Best for

WaitGo is useful when you want to:

* Queue several corrections, requests, or implementation notes before execution.
* Batch feedback after reviewing a first result.
* Avoid Claude Code starting too early.
* Let Claude Code reorganize related requests, dependencies, or conflicts before acting.

## How to use

When you want to stage several requests in a Claude Code session, type:

```txt
/wait-go
```

## What the command does

When you run `/wait-go`, Claude enters a waiting mode and lets you send several instructions in a row.

Before you write `go`, Claude does not start any task, modify files, produce a detailed analysis, or propose an execution plan. It only confirms that the instruction has been received and keeps it in memory.

When you write exactly `go`, Claude rereads all received instructions, groups them into coherent blocks, identifies dependencies, ambiguities, or possible conflicts, proposes a clear execution order, and processes the tasks step by step.

At the end, Claude provides a concise summary of what was done, the execution order followed, and the list of files created or modified.

## How is this different from plan mode?

Plan mode helps Claude think before acting.

WaitGo is for a different moment: when you already have several corrections, notes, or implementation requests to send, but you do not want Claude to start after the first one.

It lets you stage all your feedback first, then trigger one consolidated execution with `go`.

## Limitations

WaitGo does not bypass Claude Code permissions.

If Claude Code needs approval to read, edit, run, or access something, the usual permission prompts still apply. WaitGo only changes when Claude starts processing your instructions; it does not change what Claude is allowed to do.

## Install in Claude Code

### Method 1: Copy the command file

Copy [wait-go.md](.claude/commands/wait-go.md) into your project's `.claude/commands/` folder.

### Method 2: Install using Claude Code

You can ask Claude Code to handle the installation. Paste this prompt in a Claude Code session:

[install-waitgo-for-claude-code.md](prompts-for-installation/install-waitgo-for-claude-code.md)

## Install and use in Codex

WaitGo includes a native Codex skill in [`.agents/skills/waitgo`](.agents/skills/waitgo) and a legacy slash-prompt compatibility file in [`.codex/prompts/waitgo.md`](.codex/prompts/waitgo.md).

For a global installation backed by this repository, link both entry points into your Codex home:

```sh
mkdir -p "$HOME/.codex/skills" "$HOME/.codex/prompts"
ln -s "$PWD/.agents/skills/waitgo" "$HOME/.codex/skills/waitgo"
ln -s "$PWD/.codex/prompts/waitgo.md" "$HOME/.codex/prompts/waitgo.md"
```

Restart Codex or open a new chat, then invoke the recommended native skill:

```txt
$waitgo
```

Codex's deprecated custom-prompt mechanism is also available as:

```txt
/prompts:waitgo
```

Codex reserves root slash commands and does not currently support a custom `/waitgo` alias. `$waitgo` is the native reusable form and works across projects.

### Install using Codex

You can also ask Codex to handle the installation in the current project. Paste this prompt in a Codex session:

[install-waitgo-for-codex.md](prompts-for-installation/install-waitgo-for-codex.md)

## Using with other AI assistants

This repo is designed primarily for Claude Code. The same behavior can be reproduced with other AI assistants using the instructions in:

[install-waitgo-for-any-ai.md](prompts-for-installation/install-waitgo-for-any-ai.md)

Paste these instructions into the target assistant to let it recreate the WaitGo behavior in its own supported format.

## Use in a regular AI chat (ChatGPT, Claude, Gemini…)

If you just want to use WaitGo inside a normal chat, not install it in a coding assistant or project environment, copy this version into a new conversation:

[waitgo-ai-chat-version.md](prompts-for-ai-chat/waitgo-ai-chat-version.md)

It only applies to the current chat. If you start a new conversation, paste it again.

## Repository structure

```txt
wait-go/
├── README.md
├── LICENSE
├── .gitignore
├── .agents/
│   └── skills/
│       └── waitgo/
│           ├── SKILL.md
│           └── agents/
│               └── openai.yaml
├── .codex/
│   └── prompts/
│       └── waitgo.md
├── .claude/
│   └── commands/
│       └── wait-go.md
├── prompts-for-ai-chat/
│   └── waitgo-ai-chat-version.md
├── prompts-for-installation/
│   ├── install-waitgo-for-claude-code.md
│   ├── install-waitgo-for-codex.md
│   └── install-waitgo-for-any-ai.md
└── public/
    ├── waitgo-demo.mp4
    ├── waitgo-demo-1500w-24fps.gif
    └── waitgo-image.png
```
