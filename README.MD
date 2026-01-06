# JIBS Thesis Template

This repository contains a LaTeX template that aims to match the official MSWord JIBS thesis projects' template.
[See the original .docx template here.](https://ju.se/student/en/studies/thesis-examination-paper.html)

## Overview

- The template uses 1 inch margins, 12pt. font, a typeface very similar to Times New Roman, 1.5 line spacing.
- Build files and output are found in the `build` directory.
- APA style referencing via `biblatex`
- Clickable Table of Contents, List of Figures, List of Tables
- Consistent heading hierarchy (Chapter/ Section/ Subsection/ Subsubsection) and formatting
- Chapter abstracts
- Appendix support
- Macros for tables, figures, and chapter abstracts

## Structure

```text
├── main.tex                # Entry point
├── preamble.tex            # Packages and global formatting
├── config/
│   ├── personal_info.tex   # Author, title, degree info
│   └── frontpage_info.tex  # Abstract page information
├── macros/
│   ├── table.tex
│   ├── figure.tex
│   └── chapter_abstract.tex
├── figures/                # Charts, pictures, etc.
├── chapters/
│   ├── introduction.tex
│   └── literature_review.tex
├── appendix/
│   └── appendix_a.tex
├── references.bib
├── assets/
│   └── jibs-logo.png
├── build/                  # Generated files (gitignored)
└── example_output.pdf
```

## Compilation
```bash
latexmk -pdf -output-directory=build main.tex
```

If using VSCode, a `.vscode/` directory is included with a `settings.json` that has the appropriate settings for auto formatting and build-on-save in VSCode (make sure you have the LaTeX Workshop extension) -- if not using VSCode, this is safe to delete or ignore.

## How to write content

Chapters are found in `chapters/`. To create a new one do this:

- Create a file in `chapters/` with an appropriate name and `.tex` extension, like `methodology.tex`.
- Create a new input in `main.tex`.
- Write `\chapter{**chapter-name**}` at the top of the newly created file.
- Optionally use `\ChapterAbstract{}`.

```tex
%% main.tex
\input{chapters/methodology.tex}

%% chapters/methodology.tex
\chapter{Methodology}

\ChapterAbstract{Your chapter abstract...}

Your content
```

## How to use the provided macros

This template defines several helper macros to ensure consistent formatting for common thesis elements.
**Do not redefine these macros in chapter files** -- use them as documented below or define completely new separate ones.


### Chapter Abstracts

Each chapter can begin with a short abstract that summarizes its contents.

#### Macro

```latex
\ChapterAbstract{<text>}
```

#### Purpose

* Displays a short italicized paragraph at the start of a chapter
* Visually separated from the main text
* Intended to give the reader an overview of the chapter

#### Example

```latex
\chapter{Introduction}

\ChapterAbstract{
The purpose of this chapter is to introduce the research topic, provide background context, and outline the structure of the thesis.
}

This chapter begins by discussing…
```

---

### Figures

Figures should be inserted using the `\Figure` macro to ensure consistent sizing, captions, and placement.

#### Macro

```latex
\Figure[<width>]{<image path>}{<caption>}{<label>}
```

#### Arguments

| Argument       | Description                                                 |
| -------------- | ----------------------------------------------------------- |
| `[<width>]`    | *(Optional)* Width of the figure (default: `0.8\textwidth`) |
| `<image path>` | Path to the image file                                      |
| `<caption>`    | Caption text shown below the figure                         |
| `<label>`      | Label used for `\ref{}` (can be left empty if not needed)   |

#### Example (default size)

```latex
\Figure{figures/model.png}{Conceptual research model}{fig:research-model}
```

#### Example (custom size)

```latex
\Figure[0.5\textwidth]{figures/icon.png}{Program icon}{fig:icon}
```

#### Referencing a figure in text

```latex
As shown in Figure~\ref{fig:research-model}, the variables are related…
```

---

### Tables

Tables should be wrapped in the `ThesisTable` environment to maintain consistent layout and spacing.

#### Environment

```latex
\begin{ThesisTable}{<caption>}{<label>}
    % table content
\end{ThesisTable}
```

#### Purpose

* Ensures consistent captions and font sizing
* Encourages clean, borderless tables
* Works well with the `booktabs` package

#### Example

```latex
\begin{ThesisTable}{Descriptive statistics}{tab:descriptive}
\begin{tabular}{lccc}
\toprule
Variable & Mean & Std. Dev. & N \\
\midrule
Income   & 45.2 & 12.1      & 120 \\
Age      & 34.5 & 8.9       & 120 \\
\bottomrule
\end{tabular}
\end{ThesisTable}
```

#### Referencing a table

```latex
Table~\ref{tab:descriptive} presents the descriptive statistics.
```

---

### Table Notes

Use `\TableNote` to add optional notes below a table (e.g., data sources or explanations).

#### Macro

```latex
\TableNote{<note text>}
```

#### Example

```latex
\begin{ThesisTable}{Regression results}{tab:regression}
\begin{tabular}{lcc}
\toprule
Variable & Coefficient & p-value \\
\midrule
Education & 0.45 & 0.01 \\
Experience & 0.32 & 0.03 \\
\bottomrule
\end{tabular}
\end{ThesisTable}

\TableNote{Notes: Standard errors in parentheses. Data from Statistics Sweden.}
```

---

### General Guidelines

* Use the provided macros instead of raw `figure` or `table` environments
* Always supply a label if you plan to reference the object
* Keep content (text) separate from formatting (handled by the template)

---

### Front Page Macro Usage

The template provides a macro called `\Frontpage` that automatically generates the full front matter page, including:

* Degree/Program information
* Title, authors, tutor, and date
* Key terms
* Abstract (optionally structured or running text)

All content is configurable through commands in `config/frontpage_info.tex`, allowing you to fill in your personal details without touching the macro itself.

#### Configurable Commands

You can define or update these in `config/frontpage_info.tex`:

```latex
% --- Degree / Program ---
\newcommand{\FrontpageDegree}{\LARGE Bachelor/Master Thesis/Degree Project in Business Administration/ Economics/ Informatics/ General Management (select which is appropriate)}

% --- Title, authors, tutor, date ---
\newcommand{\FrontpageTitle}{\ThesisTitle}        % Use the raw title text
\newcommand{\FrontpageAuthors}{\ThesisAuthors}   % e.g., "Alice A. and Bob B."
\newcommand{\FrontpageTutor}{\ThesisSupervisor} % Supervisor name(s)
\newcommand{\FrontpageDate}{\ThesisLocation, \ThesisDate}

% --- Keywords ---
\newcommand{\FrontpageKeywords}{Provide 4-6 key words that are an integral part of your study}

% --- Abstract Options ---
\newcommand{\FrontpageAbstractOptionOne}{%
    \begin{tabular}{@{}ll@{}}
        \textbf{Background:} & Background \\
        \textbf{Purpose:}    & Purpose    \\
        \textbf{Method:}     & Method     \\
        \textbf{Conclusion:} & Conclusion
    \end{tabular}
}

\newcommand{\FrontpageAbstractOptionTwo}{%
    XXX is an important theme in Entrepreneurial research.
    The purpose of the study was to ...
    The study was based on the theory of XXX and a XXX methodology was followed.
    The findings show that ... .
    Organisations can use these findings to ...
}
```

### Using the Macro

Simply include the macro in your main document **after loading the frontpage configuration**:

```latex
\input{config/frontpage_info.tex}  % load your frontpage info
\Frontpage                           % generate the front page
```

### Choosing Abstract Option

By default, the macro uses `\FrontpageAbstractOptionOne`.
You can switch to `OptionTwo` by commenting/uncommenting in `macros/frontpage.tex`.


---



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

## Licensing/Credit
This template is provided under the MIT License.
You are free to use and modify it for academic work.
Attribution is appreciated but not required.