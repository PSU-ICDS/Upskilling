# CLAUDE.md — guide for Claude (Sonnet) maintaining this repository

This file tells an AI assistant (Claude Sonnet) how to help maintain the **AI Upskilling Resources** repository. A human maintainer gives the final review and merge. Your job is to do the mechanical work accurately and keep everything consistent and accessible.

## What this repository is

A public, community-curated collection of AI learning resources for the Penn State community, maintained by ICDS. Contributors are faculty, many from non-technical disciplines. Entries are peer reviews: each names a real person and gives a recommendation. Keep the tone welcoming and the barrier to entry low.

## Golden rules

1. **Never invent reviews, names, or recommendations.** Only record what a real person actually submitted. If a submission is missing a name or recommendation, flag it for the maintainer rather than guessing.
2. **Do not edit or reword someone's review substance.** Fix obvious typos and formatting, but keep their voice and verdict.
3. **Preserve existing entries.** When adding, insert; do not overwrite or reorder other people's contributions except to keep a page alphabetical.
4. **A human merges.** Propose changes (a branch, a patch, or a clearly marked edit). Do not assume authority to publish unilaterally.
5. **Accessibility is not optional.** Every change must keep the repository at WCAG 2.2 AA. See `ACCESSIBILITY.md` and the checklist below.

## Repository layout

```
README.md                     Landing page, featured list, how to contribute
LICENSE.md                    CC BY-SA 4.0
CONTRIBUTING.md               How faculty add resources (PR, form, issue, email)
ACCESSIBILITY.md              WCAG 2.2 AA commitment and authoring rules
CODE_OF_CONDUCT.md            Community guidelines
MAINTAINERS.md                Maintainer workflow
CLAUDE.md                     This file
.gitignore
.github/
  PULL_REQUEST_TEMPLATE.md
  ISSUE_TEMPLATE/
    suggest-resource.yml      Guided issue form
    config.yml
resources/
  README.md                   Category index
  courses/README.md
  tutorials-and-guides/README.md
  ai-models/README.md
  ai-tools-and-harnesses/README.md
  books-and-articles/README.md
  videos-and-talks/README.md
  community-repos/README.md
templates/
  resource-entry-template.md
  resource-detail-page-template.md
details/
  example-detail-page.md      Example of a longer write-up
```

## The entry format (canonical)

Every resource entry follows this shape. The source of truth is `templates/resource-entry-template.md`; match it exactly.

```markdown
### [Short title](https://link)

**Level:** Beginner · **Modality:** Text, Video · **Purpose:** Research, Productivity

**Reviews:**

- MM/YYYY or YYYY — **Reviewer Name** — Highly Recommend. Optional sentence or two.

_More info: [optional detail page](../../details/some-page.md)_
```

Controlled vocabularies (do not introduce new values without maintainer sign-off):

- **Level:** Beginner, Intermediate, Advanced, Expert
- **Modality:** Text, Code, Images, Audio, Video
- **Purpose:** Coding, Research, Productivity
- **Recommendation:** Highly Recommend, Recommend, Neutral, Do Not Recommend
- **Date:** YYYY, or MM/YYYY for more precision

## Common tasks and how to do them

### Add a new resource

1. Identify the best category. If ambiguous, choose the closest and note the alternative for the maintainer.
2. Open that category's `README.md`.
3. Insert a new entry using the canonical format, placed alphabetically by title.
4. Fill Level, Modality, Purpose, and the reviewer's name, recommendation, and note from the submission verbatim (light copyedit only).
5. If the resource plausibly belongs on the home page "Start here" list (a broadly useful beginner resource), suggest that to the maintainer rather than adding it there yourself.

### Add a review to an existing resource

1. Find the existing entry. Do **not** create a second entry for the same resource.
2. Add one bullet under its `**Reviews:**` list with the new person's name, recommendation, and note.

### Transcribe a submission (issue, form, or email)

Map submission fields to the template: title and link, category, level, modality (may be several), purpose (may be several), reviewer name, recommendation, and note. Verify the link resolves. If a required field is missing, list what is missing and ask the maintainer or the submitter rather than filling it in yourself.

### Add a file a faculty member sent

1. Confirm with the maintainer that sharing rights and CC BY-SA 4.0 are acknowledged.
2. Place the file in a `files/` subfolder within the relevant category (create it if needed), with a descriptive filename.
3. Add a normal entry that links to the file with a relative path and credits the author.

### Incorporate a whole repository

Default to a link-only entry in `resources/community-repos/README.md`. Only propose a git submodule when the maintainer asks; describe the exact `git submodule add` command (see `MAINTAINERS.md`) rather than running anything destructive. Always record the source repository's own license in the entry.

### Create a detail page

Use `templates/resource-detail-page-template.md`. Save it in `details/` with a descriptive filename, then add a `_More info:_` link from the entry.

## Accessibility checklist (run on every change)

- Link text describes the destination (no "click here", no bare URLs as the only link text).
- Tags are plain words, never conveyed by color or icon alone.
- Any image has descriptive alt text (`![description](path)`); decorative images use empty alt text.
- Headings are in order and do not skip levels.
- New tables have a header row; avoid merged cells and nested tables. Prefer bulleted entries over dense tables.
- Acronyms are spelled out on first use.

## Voice and tone

Warm, plain, and encouraging. Write for faculty from any discipline, including people new to AI. Short sentences. Avoid jargon, or explain it. Follow the Penn State preference to reserve technical detail for where it helps. This repository's own style (see `ICDS/CLAUDE.md` in the wider workspace if present) favors clarity for both technical and non-technical audiences, active voice, and concrete examples.

## What to hand back to the maintainer

When you finish a change, summarize: what you added or edited, which files changed, any fields that were missing or ambiguous, and anything you were unsure about (a category choice, a possible duplicate, a link that did not resolve). Keep it short. The maintainer reviews and merges.

## What not to do

- Do not fabricate content, reviews, names, or endorsements.
- Do not delete or substantively rewrite others' contributions.
- Do not add resources that are advertising, off-topic, or that require re-hosting copyrighted material (link instead).
- Do not publish without a human maintainer's review.
- Do not introduce new tag values or change the entry format without maintainer approval.
