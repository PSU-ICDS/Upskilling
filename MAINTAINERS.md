# Maintainer guide 

This page is for maintainers who keeps the repository tidy. Contributors do not need to read it. The aim is to make maintenance quick and low-stress.

**Audience:** Internal

## Your regular tasks

Most weeks, maintenance is three things: merge pull requests, transcribe submissions that came in by issue, form, or email, and keep the categories tidy.

### Merge a pull request

1. Open the pull request and skim the entry. Check the four things on the PR checklist: the link works, tags are words, the review has a name and a recommendation, and link text is descriptive.
2. Fix small issues yourself by committing to the PR branch, or leave a friendly comment asking the contributor to adjust. Faculty are volunteers; keep feedback kind and short.
3. Click **Merge**. Done. GitHub renders the updated page immediately.

### Transcribe an issue or email submission

When someone uses the "Suggest a resource" issue form or email, the content is not yet in a file. You add it:

1. Open the relevant category page under `resources/` (for example, `resources/courses/README.md`).
2. Click the pencil (Edit) icon, paste the entry template from `templates/resource-entry-template.md`, and fill it from the submission.
3. Keep the list alphabetical by title. If the resource already exists, add the person's review as another bullet rather than duplicating the entry.
4. Commit directly to the main branch (you have write access) with a message like `Add [title] from issue #123`.
5. If it came from an issue, close the issue with a comment linking to the page.

### Add a file on someone's behalf

When a faculty member sends a file they made (slides, a handout, a notebook) and cannot use GitHub:

1. Confirm they have the right to share it and are fine with CC BY-SA 4.0.
2. Put the file in a sensible place. A good convention is a `files/` subfolder inside the most relevant category, for example `resources/tutorials-and-guides/files/`. Use a descriptive filename.
3. Add a normal entry that links to the file (a relative link) and credits the author in the review.

### Keep categories tidy

Move mis-filed entries to the right category, merge accidental duplicates, and fix broken links as you notice them. Nothing heavy; a light pass when you are already in the repository is enough.

## Incorporating a whole repository

Two options, described for contributors in `resources/community-repos/README.md`:

- **Link only (default):** just add an entry pointing to the repository. Nothing else to do.
- **Git submodule (when materials are closely tied):** from a local clone, run:

  ```bash
  git submodule add https://github.com/owner/repo resources/community-repos/repo-name
  git commit -m "Add <name> as submodule"
  git push
  ```

  This pins a reference without copying files, and the original author keeps control. Note the source repository's own license in the entry. To update the pinned version later: `git submodule update --remote resources/community-repos/repo-name`, then commit.

## Using Claude to help

`CLAUDE.md` explains how to have Claude (Sonnet) draft entries, transcribe submissions, and run consistency checks. Claude can do the mechanical parts; a maintainer still gives the final merge.

## Accessibility spot-check

When merging, glance for: descriptive link text, alt text on any images, headings in order, and header rows on any new tables. See `ACCESSIBILITY.md`. This keeps us at WCAG 2.2 AA without a heavy process.
