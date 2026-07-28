# Accessibility

This repository aims to conform to [Web Content Accessibility Guidelines (WCAG) 2.2, Level AA](https://www.w3.org/TR/WCAG22/). Because the content is written and reviewed by many people, accessibility depends on everyone following a few simple authoring habits. This page explains both our commitment and the rules for contributors.


## Authoring rules for contributors

Following these keeps us at WCAG 2.2 AA. They are quick, and most are just good writing.

### Write meaningful link text

The clickable text should describe where the link goes. This satisfies WCAG 2.4.4 (Link Purpose).

- Good: `[AI Essentials Faculty Resources](https://ai.psu.edu/...)`
- Avoid: `[click here](https://ai.psu.edu/...)` or a bare pasted URL as the link text.

### Never rely on color alone

Tags and recommendations are always written as words (`Beginner`, `Highly Recommend`), never conveyed only by a color or an icon. This satisfies WCAG 1.4.1 (Use of Color). If you add badge images, the tag word must also appear in text or in the image's alt text.

### Give every image alt text

If you include an image (a screenshot, a diagram, a badge), provide descriptive alternative text so screen-reader users get the same information. This satisfies WCAG 1.1.1 (Non-text Content).

- In Markdown: `![Description of what the image shows](path/to/image.png)`
- For a decorative image that adds no information, use empty alt text: `![](path/to/image.png)`

### Use headings in order

Structure pages with real Markdown headings (`#`, `##`, `###`) and do not skip levels (do not jump from `##` to `####`). Screen-reader users navigate by headings, so a logical outline matters. This supports WCAG 1.3.1 (Info and Relationships) and 2.4.6 (Headings and Labels).

### Keep tables simple and give them header rows

Use a header row for every table so assistive technology can associate data with its column. Avoid merged cells and tables-within-tables. When a comparison would be complex, prefer a bulleted list of entries over a dense table. This supports WCAG 1.3.1.

### Write in plain, clear language

Spell out acronyms on first use (for example, "large language model (LLM)"). Short sentences and everyday words help everyone, including non-native English speakers and people with cognitive disabilities. This supports WCAG 3.1 guidelines on readability.

### Use descriptive file and page names

Name files and detail pages so their purpose is clear from the name alone (for example, `claude-code-getting-started.md`, not `page2.md`).

## Why we prefer text tags over image badges

Image badges (the small colored labels common on GitHub) can look nice, but they carry meaning through color and require correct alt text to be accessible, and they are harder for non-technical faculty to edit. For those reasons this repository uses **plain-text tags** as the default. Contributors who want image badges may add them, but only alongside the text tag, never as a replacement.

## Testing and review

Maintainers do a light accessibility check when merging: descriptive link text, alt text on any images, sensible heading order, and header rows on tables. GitHub's own Markdown rendering handles color contrast and responsive layout, so most of the burden is on the writing, which these rules cover.

## Standard referenced

WCAG 2.2 was published as a W3C Recommendation. Level AA is the conformance level commonly required for public-sector and university content. The full guidelines are at <https://www.w3.org/TR/WCAG22/>.

## Report challenges

We want every member of the Penn State community to be able to read, navigate, and contribute to this repository, including people who use screen readers, keyboard-only navigation, screen magnification, or high-contrast settings. If you encounter a barrier, please open an issue or email `icds@psu.edu` with the subject line "AI Upskilling Learning Repository: Accessibility"
