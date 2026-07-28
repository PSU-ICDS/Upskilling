# Contributing a resource

Thank you for helping other Penn State faculty find their footing with AI. This page explains how to add a learning resource, no matter how comfortable you are with GitHub. Every path ends with the same result: your recommendation, with your name on it, helping a colleague.

## What makes a good entry

You do not need to write much. A complete entry has:

1. A **short title** with a link to the resource.
2. A few **tags**: a level, one or more modalities, and one or more purposes (explained below).
3. **Your name**, the **date** of your recommendation (`YYYY` or `MM/YYYY`), and a **recommendation** (`Highly Recommend`, `Recommend`, `Neutral`, or `Do Not Recommend`).
4. Optionally, **a sentence or two** on why, and a link to a detail page with more information.

If a resource is already listed and you have used it too, please add your own review rather than creating a duplicate entry. Multiple opinions on the same resource are welcome and genuinely useful.

## The tags

Pick whatever fits. When in doubt, guess, a maintainer can adjust it.

- **Level:** `Beginner`, `Intermediate`, `Advanced`, `Expert`
- **Modality:** `Text`, `Code`, `Images`, `Audio`, `Video`
- **Purpose:** `Coding`, `Research`, `Productivity`
- **Recommendation:** `Highly Recommend`, `Recommend`, `Neutral`, `Do Not Recommend`
- **Date:** `YYYY`, or `MM/YYYY` for more precision

Tags are always written as plain words, never as color alone, so the repository stays accessible to everyone. See [ACCESSIBILITY.md](ACCESSIBILITY.html).

## The entry format

Copy the block from [templates/resource-entry-template.md](templates/resource-entry-template.md) and fill it in. It looks like this:

```markdown
### [Short title of the resource](https://example.com/link)

**Level:** Beginner · **Modality:** Text, Video · **Purpose:** Research, Productivity

**Reviews:**

- MM/YYYY or YYYY — **Your Name** — Highly Recommend. One or two sentences on why this was useful.

_More info: [optional detail page](../../details/example-detail-page.md)_
```

Add your entry under the right category heading. If a resource could fit several categories, pick the closest one.

---

## Choose your path

### Path 1: Pull request (if you are comfortable with GitHub)

This is the fastest path and needs no maintainer transcription. It works entirely in your web browser, or from the command line if you prefer working locally.

#### Repository structure

This repository is plain Markdown, browsable and editable right on GitHub, no build step or local tooling required. Resource entries live in the category pages under `resources/` (for example, `resources/courses/README.md`); detail pages live under `details/`; and the entry template lives at `templates/resource-entry-template.md`. There is no staging branch: pull requests are opened directly against `main`, and GitHub renders the updated Markdown as soon as a maintainer merges.

#### Quick edit in your browser

1. Navigate to the category page you want to edit, for example [resources/courses/README.md](resources/courses/README.md).
2. Click the **pencil (Edit)** icon in the top-right of the file view. If you do not have write access, GitHub automatically creates a fork for you behind the scenes.
3. Paste in the entry template and fill it out. Keep entries in the file grouped sensibly (alphabetical by title is fine).
4. Scroll down, choose **"Create a new branch for this commit and start a pull request,"** and click **Propose changes**.
5. Add a short title for your pull request and submit it. A maintainer will review and merge it.

A pull request template will prompt you for the same information, so you cannot really get it wrong.

#### Working from your own fork (for Git users who prefer to work locally)

If you would rather edit files on your own machine, or you are contributing several entries at once:

1. Create your own fork of the `PSU-ICDS/AI-Upskilling-Resources` repository ([how to fork a repo](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)).
2. Clone your fork locally and create a branch for your changes.
3. Add or edit entries in the relevant `resources/<category>/README.md` file, following the [entry format](#the-entry-format) above. Since this is plain Markdown, you can preview it in any Markdown viewer or editor; no local build is needed.
4. Commit and push your branch to your fork.
5. Open a pull request from your branch to the `main` branch of this repository ([how to create a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)). A maintainer will review and merge it.

New to Git and want to learn more? We recommend the ["Version Control with Git" lesson](https://swcarpentry.github.io/git-novice/) from [The Carpentries](https://carpentries.org/).

### Path 2: GitHub Issue (a guided prompt, still no file editing)

If you have a GitHub account but do not want to edit files:

1. Go to the **Issues** tab of this repository.
2. Click **New issue** and choose **"Suggest a resource."**
3. Fill in the fields (title, link, tags, your recommendation, and a note). Submit.

A maintainer will turn your issue into a proper entry.

### Path 3: Email the ICDS (no GitHub at all)

If GitHub is not for you, just send the details by email:

> **Email:** `icds@psu.edu` with the subject line **"AI Upskilling Learning Repository: Suggestion"**

Include the title, the link, your recommendation, and a sentence about why. If you developed a file yourself (a slide deck, a handout, a notebook) and want it hosted here, attach it and let us know how you would like to be credited.

---

## Sharing a whole repository

If you have an entire GitHub repository of materials, we can link it or incorporate it. See [resources/community-repos/README.md](resources/community-repos/README.md) for how we handle these, including the option to add it as a git submodule. Mention this in your pull request, issue, or email and a maintainer will help.

## Licensing your contribution

By contributing, you agree that your original contributions are licensed under [CC BY-SA 4.0](LICENSE.html), and you confirm you have the right to share what you submit. Linking to a public resource is always fine. Uploading someone else's copyrighted material is not, so link to it instead.

## Helpful links

- [Markdown Guide](https://www.markdownguide.org/)
- [How to create a fork in GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)
- [How to create a pull request in GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
- ["Version Control with Git" (The Carpentries)](https://swcarpentry.github.io/git-novice/)

## Questions

Email the ICDS Upskilling list at `icds@psu.edu` with the subject line "AI Upskilling Learning Repository: Suggestion"
