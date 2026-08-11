# CLAUDE.md — guide for Claude (Sonnet) maintaining this repository

This file tells an AI assistant (Claude Sonnet) how to help maintain the **ICDS Upskilling Resources** repository. A human maintainer gives the final review and merge. Your job is to do the mechanical work accurately and keep everything consistent and accessible.

## What this repository is

A public, community-curated collection of learning resources for the Penn State community, maintained by ICDS. It is organized around the five ICDS research hubs: Artificial Intelligence, Computational Sciences, Data Sciences, Digital Twins, and Quantum Sciences. Contributors are faculty, many from non-technical disciplines. Entries are peer reviews: each names a real person and gives a recommendation. Keep the tone welcoming and the barrier to entry low.

The collection began as an AI-only reading list, so the Artificial Intelligence hub holds nearly all the entries today. The other four hubs are scaffolded and waiting for their first contributions.

## Golden rules

1. **Never invent reviews, names, or recommendations.** Only record what a real person actually submitted. If a submission is missing a name or recommendation, flag it for the maintainer rather than guessing.
2. **Do not edit or reword someone's review substance.** Fix obvious typos and formatting, but keep their voice and verdict.
3. **Preserve existing entries.** When adding, insert; do not overwrite or reorder other people's contributions except to keep a page alphabetical.
4. **A human merges.** Propose changes (a branch, a patch, or a clearly marked edit). Do not assume authority to publish unilaterally.
5. **Accessibility is not optional.** Every change must keep the repository at WCAG 2.2 AA. See `ACCESSIBILITY.md` and the checklist below.

## Repository layout

```
README.md                     General index: what this is, the five hubs, how to contribute
LICENSE.md                    CC BY-SA 4.0
CONTRIBUTING.md               How faculty add resources (PR, form, issue, email)
ACCESSIBILITY.md              WCAG 2.2 AA commitment and authoring rules
CODE_OF_CONDUCT.md            Community guidelines
MAINTAINERS.md                Maintainer workflow
CLAUDE.md                     This file
_config.yml                   Jekyll config; the `hubs:` list drives the site nav
_includes/header.html         Nav bar, built from the `hubs:` list
contributing-page.md          Mirror pages: GitHub reserves the CONTRIBUTING.md,
license-page.md               LICENSE.md, and CODE_OF_CONDUCT.md filenames, so
code-of-conduct-page.md       these publish them at /CONTRIBUTING.html etc.
.gitignore
.github/
  PULL_REQUEST_TEMPLATE.md
  ISSUE_TEMPLATE/
    suggest-resource.yml      Guided issue form
    config.yml

ai/                           Artificial Intelligence hub
  README.md                   Hub home: start-here list, category table
  resources/
    README.md                 Category index
    courses/README.md
    tutorials-and-guides/README.md
    ai-models/README.md
    ai-tools-and-harnesses/README.md
    books-and-articles/README.md
    videos-and-talks/README.md
    community-repos/README.md
computational/                Computational Sciences hub
  README.md
  resources/README.md         Category index; no category pages yet
data/                         Data Sciences hub (same shape)
digital-twins/                Digital Twins hub (same shape)
quantum/                      Quantum Sciences hub (same shape)

templates/                    Shared across all hubs
  resource-entry-template.md
  resource-detail-page-template.md
details/                      Shared across all hubs
  example-detail-page.md      Example of a longer write-up
  pdf-to-markdown-converters.md
```

Note the folder names drop "Sciences": `computational`, `data`, and `quantum`. The display names keep it.

## The entry format (canonical)

Every resource entry follows this shape. The source of truth is `templates/resource-entry-template.md`; match it exactly.

```markdown
### [Short title](https://link)

**Level:** Beginner · **Modality:** Text, Video · **Purpose:** Research, Productivity

**Reviews:**

- MM/YYYY or YYYY — **Reviewer Name** — Highly Recommend. Optional sentence or two.

_More info: [optional detail page](../../../details/some-page.md)_
```

Controlled vocabularies (do not introduce new values without maintainer sign-off):

- **Hub:** Artificial Intelligence, Computational Sciences, Data Sciences, Digital Twins, Quantum Sciences
- **Level:** Beginner, Intermediate, Advanced, Expert
- **Modality:** Text, Code, Images, Audio, Video
- **Purpose:** Coding, Research, Productivity
- **Recommendation:** Highly Recommend, Recommend, Neutral, Do Not Recommend
- **Date:** YYYY, or MM/YYYY for more precision

## Common tasks and how to do them

### Add a new resource

1. Identify the hub first, then the best category within it. If either is ambiguous, choose the closest and note the alternative for the maintainer.
2. Open that category's `README.md` at `<hub>/resources/<category>/README.md`. If the hub has no page for that category yet, create one following the shape of an existing AI hub page, and link it from `<hub>/resources/README.md`.
3. Insert a new entry using the canonical format, placed alphabetically by title.
4. Fill Level, Modality, Purpose, and the reviewer's name, recommendation, and note from the submission verbatim (light copyedit only).
5. If the resource plausibly belongs on the home page "Start here" list (a broadly useful beginner resource), suggest that to the maintainer rather than adding it there yourself.

### Add a review to an existing resource

1. Find the existing entry. Do **not** create a second entry for the same resource.
2. Add one bullet under its `**Reviews:**` list with the new person's name, recommendation, and note.

### Transcribe a submission (issue, form, or email)

Map submission fields to the template: title and link, hub, category, level, modality (may be several), purpose (may be several), reviewer name, recommendation, and note. Verify the link resolves. If a required field is missing, list what is missing and ask the maintainer or the submitter rather than filling it in yourself.

### Add a file a faculty member sent

1. Confirm with the maintainer that sharing rights and CC BY-SA 4.0 are acknowledged.
2. Place the file in a `files/` subfolder within the relevant hub's category (create it if needed), with a descriptive filename, for example `ai/resources/tutorials-and-guides/files/`.
3. Add a normal entry that links to the file with a relative path and credits the author.

### Incorporate a whole repository

Default to a link-only entry in the relevant hub's `resources/community-repos/README.md`. Only propose a git submodule when the maintainer asks; describe the exact `git submodule add` command (see `MAINTAINERS.md`) rather than running anything destructive. Always record the source repository's own license in the entry.

### Create a detail page

Use `templates/resource-detail-page-template.md`. Save it in `details/` with a descriptive filename, then add a `_More info:_` link from the entry. `details/` is shared across hubs, so name the hub at the top of the page. From a category page the relative link is `../../../details/<file>.md`.

## Accessibility checklist (run on every change)

- Link text describes the destination (no "click here", no bare URLs as the only link text).
- Tags are plain words, never conveyed by color or icon alone.
- Any image has descriptive alt text (`![description](path)`); decorative images use empty alt text.
- Headings are in order and do not skip levels.
- New tables have a header row; avoid merged cells and nested tables. Prefer bulleted entries over dense tables.
- Acronyms are spelled out on first use.

## Relative links: get the depth right

Links are relative file paths, and the hub folder added one level of nesting. From a category page at `<hub>/resources/<category>/README.md`:

- Shared root files: `../../../CONTRIBUTING.html`, `../../../ACCESSIBILITY.html`, `../../../LICENSE.html` (the `.html` mirror pages, not the `.md` files, which GitHub reserves and Jekyll does not build).
- Templates: `../../../templates/resource-entry-template.md`
- Detail pages: `../../../details/<file>.md`
- A sibling category in the same hub: `../<category>/README.md`

From a hub's `resources/README.md`, use two levels (`../../details/`); from a hub's `README.md`, use one (`../README.md`). After moving or adding a page, check every relative link in it.

## Voice and tone

Warm, plain, and encouraging. Write for faculty from any discipline, including people new to AI. Short sentences. Avoid jargon, or explain it. Follow the Penn State preference to reserve technical detail for where it helps. This repository's own style (see `ICDS/CLAUDE.md` in the wider workspace if present) favors clarity for both technical and non-technical audiences, active voice, and concrete examples.

## What to hand back to the maintainer

When you finish a change, summarize: what you added or edited, which files changed, any fields that were missing or ambiguous, and anything you were unsure about (a category choice, a possible duplicate, a link that did not resolve). Keep it short. The maintainer reviews and merges.

## What not to do

- Do not fabricate content, reviews, names, or endorsements.
- Do not delete or substantively rewrite others' contributions.
- Do not add resources that are advertising, off-topic, or that require re-hosting copyrighted material (link instead).
- Do not publish without a human maintainer's review.
- Do not introduce new tag values, add a hub, or change the entry format without maintainer approval.
- Do not move an existing entry between hubs without maintainer approval.
