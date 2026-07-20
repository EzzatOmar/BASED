# BASED

BASED is a small, file-based project-management system for software teams and
coding agents. It replaces tickets, boards, sprints, and project-management
software with one readable index and one Markdown file per task, all stored
next to the code they describe.

The name comes from its five kinds of work:

- B ugs — something is not working as expected.
- A dditions — a feature or improvement.
- S ubtractions — removing or simplifying something.
- E xplorations — research, experiments, and open questions.
- D ebt — maintenance, tooling, CI, tests, and technical debt.

## Why use BASED?

- **No separate system to maintain.** Tasks are ordinary Markdown files in Git.
- **Context stays with the code.** Plans, decisions, logs, and supporting media
  survive hand-offs and can be reviewed with the implementation.
- **The current state is easy to scan.** `tasks/BASED.md` is a short, ordered
  index; detail lives in linked task files.
- **History is automatic.** Git records when a task changed, why it changed,
  and which code change completed it.
- **It encourages small projects.** BASED favors directness, deletion, and less
  process over a growing backlog and recurring ceremonies.

## Why it works well with coding agents

Agents perform best when the objective, relevant files, decisions, and progress
are explicit. A BASED task file gives an agent a durable place to load that
context and keep it current. A new agent can continue from the plan, TODOs,
notes, and logs without reconstructing the entire conversation that created the
task.

Because the system is made of files, agents can search it with the same tools
they use for source code, update it in the same change, and follow links directly
to relevant implementation files. There is no board API, browser session, or
account required.

## Add BASED to a repository

The easiest setup is to paste the prompt below into your coding agent while it
is working in the repository you want to configure.

```text
Adopt the BASED file-based project-management system in this repository.

Use the canonical template at:
https://raw.githubusercontent.com/EzzatOmar/BASED/main/tasks/BASED.md

Do the following:

1. Inspect this repository's existing instructions and conventions first. Do
   not overwrite an existing task system or unrelated changes.
2. Create `tasks/BASED.md` from the canonical template. If `tasks/BASED.md`
   already exists, merge carefully instead of replacing it.
3. Create the category directories `tasks/b`, `tasks/a`, `tasks/s`, `tasks/e`,
   and `tasks/d`. Add `.gitkeep` to an otherwise empty category directory so it
   is preserved by Git.
4. Make task images and videos local to their task: place each asset beside its
   task Markdown file, embed it in that file, and never rely on a temporary or
   external URL when a local copy can be kept.
5. Ensure Git LFS is installed and initialized. Configure `.gitattributes` so
   common image and video formats below `tasks/` are stored with Git LFS. Do not
   rewrite existing Git history. If matching files are already committed
   outside LFS, report them and ask before running any LFS migration.
6. Detect this machine's operating system and package manager. Choose and
   install appropriate CLI compressors for the task media formats used in this
   repository (for example: oxipng for PNG, jpegoptim or mozjpeg for JPEG,
   cwebp for WebP, gifsicle for GIF, and ffmpeg for video). Install and verify at
   least one image compressor and one video compressor; add format-specific
   tools only when useful here. Follow the repository's approval policy before
   installing software.
7. In the `Inline Plan Visuals` section of `tasks/BASED.md`, replace the media
   tool placeholders with a short `Media tools in this repository` note. Name
   each verified tool and give an exact copy-paste compression command that is
   safe for this repository. Require task media to be compressed before commit.
8. Verify the resulting folder structure, Git LFS patterns, and compressor
   commands. Summarize every file changed and any setup that still needs a
   human decision.

Keep the setup small. Do not add a service, dependency, automation, or new
workflow unless it is needed for the requirements above.
```

### Manual setup

If you prefer to do it yourself, copy [`tasks/BASED.md`](tasks/BASED.md) into
your repository, create the five category directories, install
[Git LFS](https://git-lfs.com/), and add the patterns from this repository's
[`.gitattributes`](.gitattributes) to your own. Then replace the media-tool
placeholders in `BASED.md` with commands that are installed and verified on
your machine.

Git does not preserve empty directories, so keep a `.gitkeep` file in any empty
category directory. Compression and LFS solve different problems: compression
keeps each asset small, while LFS keeps large binary contents out of normal Git
objects. Use both for task images and videos.

## Daily use

1. Add a short entry to the appropriate category in `tasks/BASED.md`.
2. Create the linked task file in that category directory.
3. Keep the task's context, plan, TODOs, notes, logs, and media in the leaf file.
4. Update its status as work progresses.
5. Keep the leaf file as durable history after the work is complete.

The complete conventions and task-file template live in
[`tasks/BASED.md`](tasks/BASED.md).

## License

BASED is available under the [MIT License](LICENSE).
