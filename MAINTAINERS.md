# Maintainer guide 

This page is for maintainers who keeps the repository tidy. Contributors do not need to read it. The aim is to make maintenance quick and low-stress.

**Audience:** Internal

## The five hubs

Resources are organized by the five ICDS research hubs, each a top-level folder:

| Hub | Folder |
|---|---|
| Artificial Intelligence | `ai/` |
| Computational Sciences | `computational/` |
| Data Sciences | `data/` |
| Digital Twins | `digital-twins/` |
| Quantum Sciences | `quantum/` |

Every hub has the same shape: `<hub>/README.md`, `<hub>/resources/README.md`, and one page per category at `<hub>/resources/<category>/README.md`. Only the Artificial Intelligence hub has category pages so far; the other four have a hub page and a category index, and you create category pages as entries arrive.

### Create a category page for a hub

When the first entry for a category lands in a hub that has no page for it:

1. Create `<hub>/resources/<category>/README.md`.
2. Give it front matter with a `title:` line, a level-1 heading, and a one-line description of the category. Copy the shape of an existing page such as `ai/resources/courses/README.md`.
3. Add the entry, then link the new page from `<hub>/resources/README.md`.
4. If the hub is getting its first entry ever, remove the "No entries yet" section from `<hub>/README.md`.

### Add a hub to the site navigation

The nav bar is built from the `hubs:` list in `_config.yml`, which `_includes/header.html` loops over. Adding a hub there is all it takes; nothing else needs editing.

## Your regular tasks

Most weeks, maintenance is three things: merge pull requests, transcribe submissions that came in by issue, form, or email, and keep the categories tidy.

### Merge a pull request

1. Open the pull request and skim the entry. Check the four things on the PR checklist: the link works, tags are words, the review has a name and a recommendation, and link text is descriptive.
2. Fix small issues yourself by committing to the PR branch, or leave a friendly comment asking the contributor to adjust. Faculty are volunteers; keep feedback kind and short.
3. Click **Merge**. Done. GitHub renders the updated page immediately.

### Transcribe an issue or email submission

When someone uses the "Suggest a resource" issue form or email, the content is not yet in a file. You add it:

1. Open the relevant category page under the right hub (for example, `ai/resources/courses/README.md`).
2. Click the pencil (Edit) icon, paste the entry template from `templates/resource-entry-template.md`, and fill it from the submission.
3. Keep the list alphabetical by title. If the resource already exists, add the person's review as another bullet rather than duplicating the entry.
4. Commit directly to the main branch (you have write access) with a message like `Add [title] from issue #123`.
5. If it came from an issue, close the issue with a comment linking to the page.

### Add a file on someone's behalf

When a faculty member sends a file they made (slides, a handout, a notebook) and cannot use GitHub:

1. Confirm they have the right to share it and are fine with CC BY-SA 4.0.
2. Put the file in a sensible place. A good convention is a `files/` subfolder inside the most relevant category, for example `ai/resources/tutorials-and-guides/files/`. Use a descriptive filename.
3. Add a normal entry that links to the file (a relative link) and credits the author in the review.

### Keep hubs and categories tidy

Move mis-filed entries to the right hub or category, merge accidental duplicates, and fix broken links as you notice them. Nothing heavy; a light pass when you are already in the repository is enough.

## Incorporating a whole repository

Two options, described for contributors in each hub's `resources/community-repos/README.md`:

- **Link only (default):** just add an entry pointing to the repository. Nothing else to do.
- **Git submodule (when materials are closely tied):** from a local clone, run:

  ```bash
  git submodule add https://github.com/owner/repo ai/resources/community-repos/repo-name
  git commit -m "Add <name> as submodule"
  git push
  ```

  This pins a reference without copying files, and the original author keeps control. Note the source repository's own license in the entry. To update the pinned version later: `git submodule update --remote ai/resources/community-repos/repo-name`, then commit.

## Using Claude to help

`CLAUDE.md` explains how to have Claude (Sonnet) draft entries, transcribe submissions, and run consistency checks. Claude can do the mechanical parts; a maintainer still gives the final merge.

## Accessibility spot-check

When merging, glance for: descriptive link text, alt text on any images, headings in order, and header rows on any new tables. See `ACCESSIBILITY.md`. This keeps us at WCAG 2.2 AA without a heavy process.
