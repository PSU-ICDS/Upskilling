# Resource entry template

Copy the block below, paste it under the right category page in [`resources/`](../resources/README.md), and fill it in. Delete the guidance lines you do not need. Keep entries alphabetical by title within a page.

## The block to copy

```markdown
### [Short title of the resource](https://link-to-the-resource)

**Level:** Beginner · **Modality:** Text · **Purpose:** Research

**Reviews:**

- MM/YYYY or YYYY — **Your Name** — Highly Recommend. One or two sentences on why this was useful.

_More info: [optional detail page](../../details/your-detail-page.md)_
```

## Filling it in

**Title and link.** Keep the title short and descriptive. The linked text should say where it goes (avoid "click here").

**Level** — how much background it assumes. Choose one: `Beginner`, `Intermediate`, `Advanced`, `Expert`.

**Modality** — the kind of content. Choose one or more, comma-separated: `Text`, `Code`, `Images`, `Audio`, `Video`.

**Purpose** — what you would use it for. Choose one or more: `Coding`, `Research`, `Productivity`.

**Reviews** — one bullet per reviewer. Start with the date, then your name, then a recommendation, then an optional sentence or two:

- Date — when you made the recommendation. Use `YYYY`, or `MM/YYYY` if you want more precision.
- Recommendation options: `Highly Recommend`, `Recommend`, `Neutral`, `Do Not Recommend`.
- If the resource is already listed and you have used it, **add another bullet under the existing entry** instead of creating a duplicate. Multiple opinions are welcome.

**More info (optional).** If you want to write more (a longer review, setup notes, screenshots), create a page under [`details/`](../details) using the [detail-page template](resource-detail-page-template.md) and link it here. Otherwise delete this line.

## A filled-in example

```markdown
### [Anthropic: Learn](https://www.anthropic.com/learn)

**Level:** Beginner · **Modality:** Text, Code · **Purpose:** Coding, Productivity, Research

**Reviews:**

- 07/2026 — **First Last** — Recommend. Clear, applied intro to prompting and building simple
  workflows. Focused on one vendor's tools, so pair it with a broader overview.
- 2026 — **First Initial. Last** — Neutral. Good production values, but I wanted more on evaluating
  output quality for research use.
```

## Accessibility reminder

Write tags as words, never color alone. Give any images alt text. Keep link text descriptive. See [ACCESSIBILITY.md](../ACCESSIBILITY.md).
