
# JIBS Thesis LaTeX Template

This repository contains a LaTeX template that aims to match the official MsWord JIBS thesis projects' template.
[See the original .docx template here.](https://ju.se/student/en/studies/thesis-examination-paper.html)

> **Tip:** The latest release is always the most stable version. Check the [Releases](https://github.com/ptorpis/jibs-thesis-template/releases) tab to download a ready-to-use snapshot.

> Check out the preview: `example_output.pdf`


## Repository Structure

```text
main.tex                # Entry point
preamble.tex            # Packages and global formatting
config/                 # Personal and front page info
  ├── personal_info.tex
  └── frontpage_info.tex
macros/                 # Custom macros (figures, tables, abstracts)
  ├── table.tex
  ├── figure.tex
  └── chapter_abstract.tex
chapters/               # Thesis chapters
appendix/               # Appendices
figures/                # Charts, images, etc.
assets/                 # Logos and other static assets
build/                  # Generated PDF/output (gitignored)
references.bib          # Bibliography
example_output.pdf      # Example compiled thesis
```

> Using VSCode? A preconfigured `.vscode/settings.json` is included for build-on-save. Otherwise, you can safely ignore this.

## Writing Content

* Each chapter lives in its own file in `chapters/`.
* Create a new file (e.g., `methodology.tex`) and input it in `main.tex`:

```tex
\input{chapters/methodology.tex}
```

* Start each chapter with:

```tex
\chapter{Methodology}
\ChapterAbstract{A brief overview of this chapter.}
```

* Keep content and formatting separate: content goes in chapter files, formatting in macros/preamble.


## Macros Usage

The template provides macros for consistent formatting.

### Chapter Abstracts

```latex
\ChapterAbstract{<text>}
```

*Italicized paragraph at the start of a chapter for a summary.*

**Example:**

```latex
\chapter{Introduction}

\ChapterAbstract{
This chapter introduces the research topic and outlines the thesis structure.
}
```

### Figures

```latex
\Figure[<width>]{<image path>}{<caption>}{<label>}
```

* `[<width>]` optional (default: `0.8\textwidth`)
* `<label>` optional if referencing with `\ref{}`

**Example:**

```latex
\Figure{figures/model.png}{Conceptual research model}{fig:research-model}
\Figure[0.5\textwidth]{figures/icon.png}{Program icon}{fig:icon}
```

Reference in text:

```latex
As shown in Figure~\ref{fig:research-model}, the variables are related ... 
```

### Tables

Use `ThesisTable` environment:

```latex
\begin{ThesisTable}{<caption>}{<label>}
    % tabular content
\end{ThesisTable}
```

Optional notes:

```latex
\TableNote{Notes: Data source, clarifications, etc.}
```

**Example:**

```latex
\begin{ThesisTable}{Descriptive statistics}{tab:desc}
\begin{tabular}{lccc}
\toprule
Variable & Mean & Std. Dev. & N \\
\midrule
Income   & 45.2 & 12.1      & 120 \\
Age      & 34.5 & 8.9       & 120 \\
\bottomrule
\end{tabular}
\end{ThesisTable}

\TableNote{Notes: Data from Statistics Sweden.}
```

### Front Page

The macro `\Frontpage` generates the full front page.

**Configurable in:** `config/frontpage_info.tex`

**Commands include:**

```latex
\FrontpageDegree
\FrontpageTitle
\FrontpageAuthors
\FrontpageTutor
\FrontpageDate
\FrontpageKeywords
\FrontpageAbstractOptionOne
\FrontpageAbstractOptionTwo
```

**Usage:**

```latex
\input{config/frontpage_info.tex}
\Frontpage
```

> Switch abstract option by commenting/uncommenting the appropriate command in `macros/frontpage.tex`.


## Fonts

* Default: **Latin Modern (`lmodern`)**
* If you want a Times New Roman–like font, replace:

```tex
\usepackage{lmodern}
```

with:

```tex
\usepackage{newtxtext}
\usepackage{newtxmath}
```

Or use any other font of your choice.

## References

* APA style via `biblatex`
* Add entries in `references.bib`
* Reference entries consistently: e.g., `lastnameYear<keyword>` -> `smith2020growth`
* Use `\printbibliography` in `main.tex` for listing references.

## Best Practices (non-exhaustive list)

- Try to keep one sentence per line for easier revisions and version control.
- Use build-on-save or recompile often.
- Prefer global formatting for general rules and locally apply small changes when appropriate.
- Formatting options should be placed in `preamble.tex`.
- Let LaTeX take care of the page numbering (template already has it).
- Avoid manual spacing (`\\`, `\vspace`) .
- Avoid manual line breaks and page breaks.
- Use the provided tables and figures macros.
- For equations, use `\begin{equation}`, this lets LaTeX number the equations on a per-chapter basis automatically.
- Add all references to `references.bib`.
- Use a consistent name for the references entries, like `lastnameYear<keyword>` (keyword is optional) example: `smith2020growth`.
- Put new macros into `\macros`, avoid defining them elsewhere.
- Prefer `latexmk` for building.
- **Content in chapter files, structure in macros, formatting in the preamble.**.
- Prefer `\clearpage` over `\pagebreak`.
- Keep `main.tex` clean, organize content info separate files.
- Don't manually write personal info in places, use the `config/personal_into.tex` commands.

## Releases

* The template is **versioned with Git tags** and **GitHub releases**.
* The **latest release** is always recommended for students.
* Example: `v1.1` -> stable release with full functionality.

## Licensing

This template is provided under the **MIT License**: use, modify, and distribute freely for academic work. Attribution is appreciated but not required. Share with anyone you think could benefit from this template.

## Contact

Email: tope23on@student.ju.se