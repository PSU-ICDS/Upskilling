# PDF-to-Markdown converters

**Category:** Tutorials and guides

**Level:** Beginner · **Modality:** Text· **Purpose:** Research, Literature Search, Productivity

## What it is

Converting a PDF (a paper, report, or scanned document) into Markdown makes it easier to search, edit, and feed into AI tools and LLM-based workflows, since Markdown is plain text rather than a fixed-layout format. Several converters exist, ranging from simple command-line utilities to services built specifically for academic papers. This page collects options Fellows and the ICDS community have tried, rather than recommending a single one.

## Who it is for

Anyone who wants to feed a PDF's content to AI while reducing token usage and improving speed.  Different converters treat images, tables and references differently.

## Tools

- **[markitdown](https://github.com/microsoft/markitdown)** — Microsoft's open-source command-line tool and Python library for converting PDFs (and other file types, such as Word, PowerPoint, and HTML) to Markdown.
  - **Eric Ford** — Recommend.
- **[arxiv2md.org](http://arxiv2md.org/)** — A web service focused on converting arXiv papers to Markdown, preserving structure like sections, equations, and references.
  - **Eric Ford** — Highly Recommend.

<!--
- **[Name of the tool](https://example.com)** — One line on what it does.
  - **Your Name** — Recommend. Why it worked (or didn't) for you.
-->

## Tips and gotchas

Conversion quality varies with PDF layout: multi-column papers, scanned images, and heavy math notation are the hardest cases. 
Check the output against the original before relying on it, especially for equations and tables. 
For PDFs containing sensitive or restricted data, confirm the tool runs locally rather than uploading to a web service.

## Related

- [Tutorials and guides](../resources/tutorials-and-guides/README.md)
- [AI tools and harnesses](../resources/ai-tools-and-harnesses/README.md)

---

_Remember: descriptive link text, alt text on any images, headings in order. See [ACCESSIBILITY.md](../ACCESSIBILITY.md)._
