## Objectives 🎯

The LSMS Guidance Notes are are Word but need to be published with [Quarto](https://quarto.org/), a Markdown-driven publication tool.

## Installation 🔌

Two steps:

1. Install `pixi`
2. Run `pixi install`

The first step installs [`pixi`](https://pixi.prefix.dev/latest/), a project environment manager.
The second step install the necessary project environment: `MarkItDown`, a Office to Markdown converter, and its dependencies.

## Usage 👩‍💻

This project supports two workflows:

- [Convert](#convert). Automatically convert Word files to Markdown.
- [Finalize](#finalize). Manually perform touch-ups to Markdown, ranging from replacing mangled characters to changing or adding semantic headers.

### Convert 🪄

Before each work session, load the project environment:

```powershell
# open VSCode in the project environment
pixi run code .
```

Once the environment has been loaded:

- Open VSCode's terminal
- Convert a file using [MarkItDown's CLI interface](https://github.com/microsoft/markitdown#command-line):

```bash
markitdown 00_raw/{word_file} > {markdown_file}
```

### Finalize ✍️

Scan the document and manually correct:

- Structure
- Characters
- Footnotes
- Other content TBD

#### Structure

The Word documents often use header wrong or not at all.

When headers are wrong:

- Headers have jumps in levels (e.g., heading 1 followed by heading 4)
- Headers include counters either from Word or from the author's hard-coding (e.g., `2.1.2 Some text`)
- Headers accidentally/invisibly used (e.g., random word is an H2 heading but without any visual signal this is so)

When headers are not used, the document may need headings to demarcate levels of information and structure.

#### Characters

While automatic documention conversion from Word to Markdown is very good, the output may contain `�`. To fix these, one needs to compare the source and output documents side-by-side. From experience, these markers represent:

- Apostrophe, from a contraction or possessive
- Single or double quote
- En dash (hyphen)
- Em dash
- Math symbol

For apostrophes and quotes, these can be replaced with the corresponding keyboard character.

For the em dash, use the Markdown key combination: `---`.

For the rest, use HTML codes, preferably the expressive one (e.g., `&plusmn;`, `&times;`, etc.). See more [here](https://www.toptal.com/designers/htmlarrows/)

#### Footnotes

Use [Quarto's Pandoc-friendly footnote format](https://quarto.org/docs/authoring/markdown-basics.html#footnotes).
