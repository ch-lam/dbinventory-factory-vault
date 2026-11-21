# Rules of the Dbinventory factory's vault

This repository is the long-term memory of the Dbinventory factory's agents: what the code
and `git log` cannot say. It answers **why**, not **how**. Every agent reads it; the one holding
the Timon role `librarian` writes it, through the `doc` tasks Timon opens after each merge.

## Where it lives

The team's shared workspace clone holds this repository in `vault/` (excluded from the
workspace repository by `.git/info/exclude`); the task worktrees do not. From the clone's root,
**every path starts with `vault/`**: without the prefix, a note lands in the workspace
repository instead.

## Layout

```
CLAUDE.md                     these rules
wiki/projects/<slug>/         lessons specific to one Timon project; _index.md lists its notes
wiki/topics/<topic>.md        lessons shared by several projects, one note per topic
```

## What to write

- **Decisions** that are not obvious, with their reason (`Why:`).
- **Pitfalls** met and how they were solved.
- **Methods** worth reusing.

Never: code, diffs, activity summaries, anything `git log`, the code or the GitLab issue
already holds, guesses. One short, accurate note beats three vague ones; nothing to say means
no note.

## Format

- Language: **French**. Technical terms stay as they are.
- File names in `kebab-case.md`, named after their subject, never after the ticket.
- Front matter on every note:

  ```yaml
  ---
  type: project | topic | index
  created: YYYY-MM-DD
  tags: [tag1, tag2]
  related: ["[[other-note]]"]
  ---
  ```

  `wiki/projects/` → `project`, `wiki/topics/` → `topic`, `_index.md` → `index`.
- **Topic first**: before writing a project note, look in `wiki/topics/`. A topic that exists
  is linked and enriched; a concept that two projects share becomes a topic.
- **Links**: at least two `[[note-name]]` links in the body, both ways (B lists A in its
  `related:` when A links to B).
- **100 lines at most**: split a longer note into linked notes.
- A folder with an `_index.md` gets its line updated on every write.

## Publishing

After writing, from the clone's root:

```bash
git -C vault add -A
git -C vault commit -q -m "doc: <subject>"
git -C vault pull -q --rebase
git -C vault push -q
```

No commit when nothing was written. Never force-push, never rewrite history.
