# BASED

## Introduction

Building software is exploratory, creative, and sometimes dull and repetitive.
This document outlines how to build software in a highly technical,
small and motivated team. The goal is to minimize management
and maximize throughput. The idea behind BASED is that programming is 90% context loading and 10% actual solving and coding. Therefore we should batch work for context loading and minimize context switching.
BASED skips the traditional agile ceremonies and focuses on the codebase and a glorified to-do list.
The to-do list is the heart of the project. No tickets, no boards, no sprints, no backlog.
Just a list of things to do. The list is grouped into 5 and ordered by importance within each group.
Every developer or agent picks an item, creates its leaf file, and records the
context and work there. Once the change is merged, mark the item closed and
keep its leaf file as durable project history.

Every change in the codebase can be grouped into one of the following categories:

B ugs: Something is not working as expected.
A dditions: New features or improvements.
S ubtractions: Removing or simplifying parts of the codebase.
E xplorations: Researching new technologies or ideas.
D ebt: Internal engineering work such as CI, scripts, test automation, tooling, maintenance, and technical debt.

Statuses are tagged:

- [ ]: open
- [x]: closed
- [?]: unsure
- [!]: urgent
- [~]: in progress
- [/]: blocked

Remember to keep the codebase small. Small is clean, small is fast. Delete often.

## Structure

BASED lives at the repository root in `tasks/`.

- `tasks/BASED.md`: overview, active index, and conventions.
- `tasks/b/`: bug files.
- `tasks/a/`: addition files.
- `tasks/s/`: subtraction files.
- `tasks/e/`: exploration files.
- `tasks/d/`: debt files.

Each line in the overview stays short and links to one dedicated file.
Each dedicated file stores the task context, TODOs, notes, and logs.

## Format

Overview entries use this format:

`- [ ]: [B1](b/B1.md) - text: edit jumping`

Humans usually don't create leaf files. But agents do.

Leaf files use this format:

```md
# B1 - text: edit jumping
[Overview](../BASED.md)

<Short summary - This is read by humans. Keep it short>

## Context
<Longer explanation of the problem. Must link all relevant files.>

## Plan
<What you plan to do. Step by step plan. Use subsections>

## TODOS
<Checklist - derived from plan>
- [ ] ...

## NOTES
<Notes - Anything non trivial you discovered or want to remember>
...

### LOGS
<Logs - log any action you take>

---
```

Use the overview for scanning.
Use the leaf files for execution history and local context.
Never put a detailed plan in this file.
Never put leaf notes, lane breakdowns, execution history, or detailed task plans in this file.

## Inline Plan Visuals

Task Markdown renders images and Mermaid diagrams inline, so visuals belong in
the leaf task's `## Plan` instead of living as detached references.

- Every supplied, external, or generated image used by a task must be copied
  next to that task's markdown file and embedded inside its `## Plan` with
  normal Markdown image syntax.
- Name the first image with the exact task id: `A100.md` -> `A100.png`. Name
  additional images `A100-2.png`, `A100-3.png`, and so on. Other task types use
  the same rule, for example `B12.png` or `E5-2.png`. Do not hotlink an external
  asset when a local task-owned copy can be stored.
- Use an inline fenced `mermaid` diagram in `## Plan` for flows, ownership,
  state transitions, service relationships, or multi-step interactions.
- Substantial Addition and Exploration plans should normally include at least
  one useful inline image or Mermaid diagram. Simple one-step tasks may omit a
  visual when it would add no information.
- Visuals supplement the written plan and acceptance criteria; when they
  disagree, the written task contract is authoritative.
- Keep relevant images supplied by the user, such as bug-report screenshots, in
  the task files you create or edit.
- Track task images and videos with Git LFS. Compression is still required:
  LFS prevents binary data from bloating ordinary Git objects, while compression
  reduces the asset itself.
- Compress every image and video before committing it. Use the verified CLI
  commands recorded below.

### Media tools in this repository

Replace these placeholders during repository setup. Record only tools that are
installed and verified, and include a safe copy-paste command for each format in
use so future contributors and agents do not guess.

- Images: `<verified tool and command>`
- Videos: `<verified tool and command>`

## B ugs

<!-- Example: - [ ]: [B1](b/B1.md) - concise bug title -->

## A dditions

<!-- Example: - [ ]: [A1](a/A1.md) - concise addition title -->

## S ubtractions

<!-- Example: - [ ]: [S1](s/S1.md) - concise subtraction title -->

## E xplorations

<!-- Example: - [ ]: [E1](e/E1.md) - concise exploration title -->

## D ebt

<!-- Example: - [ ]: [D1](d/D1.md) - concise debt title -->

## Pragmatic Code Style

Long code line for lookup / easy parts.
Short code line for complex parts.
If in doubt, use long code line.

early exit > if else

Comment on complex parts.
You change code, you change comments.

pure fn > fn > static class > class

fn with side effects should have suffix ...Fx

locality of behavior, don't make me jump around

minimize redirections

dry is bad, make longer functions

factor out logic only if repeated 5 times or more
factor out only if really same logic

move types if shared into local types.ts file

types dont contain understanding, only structure, it's boilerplate, move out of sight

2 spaces for indentation
