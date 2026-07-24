# Contributing a resource

Thank you for helping other Penn State faculty find their footing with AI. This page explains how to add a learning resource, no matter how comfortable you are with GitHub. Every path ends with the same result: your recommendation, with your name on it, helping a colleague.

## What makes a good entry

You do not need to write much. A complete entry has:

1. A **short title** with a link to the resource.
2. A few **tags**: a level, one or more modalities, and one or more purposes (explained below).
3. **Your name** and a **recommendation** (`Highly Recommend`, `Recommend`, `Neutral`, or `Do Not Recommend`).
4. Optionally, **a sentence or two** on why, and a link to a detail page with more information.

If a resource is already listed and you have used it too, please add your own review rather than creating a duplicate entry. Multiple opinions on the same resource are welcome and genuinely useful.

## The tags

Pick whatever fits. When in doubt, guess, a maintainer can adjust it.

- **Level:** `Beginner`, `Intermediate`, `Advanced`, `Expert`
- **Modality:** `Text`, `Code`, `Images`, `Audio`, `Video`
- **Purpose:** `Coding`, `Research`, `Productivity`
- **Recommendation:** `Highly Recommend`, `Recommend`, `Neutral`, `Do Not Recommend`

Tags are always written as plain words, never as color alone, so the repository stays accessible to everyone. See [ACCESSIBILITY.md](ACCESSIBILITY.md).

## The entry format

Copy the block from [templates/resource-entry-template.md](templates/resource-entry-template.md) and fill it in. It looks like this:

```markdown
### [Short title of the resource](https://example.com/link)

**Level:** Beginner · **Modality:** Text, Video · **Purpose:** Research, Productivity

**Reviews:**

- **Your Name** — Highly Recommend. One or two sentences on why this was useful.

_More info: [optional detail page](../../details/example-detail-page.md)_
```

Add your entry under the right category heading. If a resource could fit several categories, pick the closest one.

---

## Choose your path

### Path 1: Pull request (if you are comfortable with GitHub)

This is the fastest path and needs no maintainer transcription. You can do it entirely in your web browser.

1. Navigate to the category page you want to edit, for example [resources/courses/README.md](resources/courses/README.md).
2. Click the **pencil (Edit)** icon in the top-right of the file view.
3. Paste in the entry template and fill it out. Keep entries in the file grouped sensibly (alphabetical by title is fine).
4. Scroll down, choose **"Create a new branch for this commit and start a pull request,"** and click **Propose changes**.
5. Add a short title for your pull request and submit it. A maintainer will review and merge it.

A pull request template will prompt you for the same information, so you cannot really get it wrong.

### Path 2: Online form (no GitHub account needed)

If you would rather fill out a form, use the ICDS resource-suggestion form:

> **Form link:** _To be added._ Until the form is live, please use Path 3 or Path 4.

The ICDS Project Management Office reviews form submissions and adds them to the repository for you, usually within a week.

### Path 3: GitHub Issue (a guided prompt, still no file editing)

If you have a GitHub account but do not want to edit files:

1. Go to the **Issues** tab of this repository.
2. Click **New issue** and choose **"Suggest a resource."**
3. Fill in the fields (title, link, tags, your recommendation, and a note). Submit.

A maintainer will turn your issue into a proper entry.

### Path 4: Email the ICDS (no GitHub at all)

If GitHub is not for you, just send the details by email:

> **Email:** `ICDS-FACULTY-UPSKILLING@lists.psu.edu` with the subject line **"Upskilling resource suggestion."**

Include the title, the link, your recommendation, and a sentence about why. If you developed a file yourself (a slide deck, a handout, a notebook) and want it hosted here, attach it and let us know how you would like to be credited.

---

## Sharing a whole repository

If you have an entire GitHub repository of materials, we can link it or incorporate it. See [resources/community-repos/README.md](resources/community-repos/README.md) for how we handle these, including the option to add it as a git submodule. Mention this in your pull request, issue, or email and a maintainer will help.

## Licensing your contribution

By contributing, you agree that your original contributions are licensed under [CC BY-SA 4.0](LICENSE.md), and you confirm you have the right to share what you submit. Linking to a public resource is always fine. Uploading someone else's copyrighted material is not, so link to it instead.

## Questions

Email the ICDS Upskilling list at `ICDS-FACULTY-UPSKILLING@lists.psu.edu`.
