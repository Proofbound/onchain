# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Quarto book project titled "The Crypto Business Solution" by Apollo Sun (孫波). The project uses the Quarto publishing system to generate HTML and PDF versions of a book from Markdown source files.

## Architecture

- **Configuration**: `_quarto.yml` defines the project structure, output formats, and book metadata
- **Content Files**: `.qmd` files contain the book chapters (index.qmd, intro.qmd, summary.qmd, references.qmd)
- **Template Config**: `cc-config.yml` contains template variables and metadata
- **Bibliography**: `references.bib` contains bibliographic references
- **Output**: `docs/` directory contains generated HTML files and assets

## Development Commands

### Building the Book
```bash
# Render the entire book to HTML and PDF
quarto render

# Preview the book with live reload during development
quarto preview

# Render only to HTML
quarto render --to html

# Render only to PDF
quarto render --to pdf
```

### Publishing
```bash
# Publish to GitHub Pages (configured for proofbound.github.io/crypto-jason/)
quarto publish gh-pages
```

## File Structure

- `index.qmd` - Book preface/landing page
- `intro.qmd` - Introduction chapter
- `summary.qmd` - Summary chapter  
- `references.qmd` - References/bibliography page
- `_quarto.yml` - Main Quarto configuration
- `cc-config.yml` - Template configuration variables
- `references.bib` - BibTeX bibliography file
- `docs/` - Generated output directory
- `*.tex` - LaTeX output files (kept due to keep-tex: true setting)

## Content Editing

Content is written in Quarto Markdown (.qmd files). Each chapter is a separate .qmd file that gets combined into the final book during rendering. The book supports:

- Cross-references between chapters
- Bibliography citations using BibTeX
- PDF and HTML output formats
- CJK font support for international characters
- Bootstrap theme (cosmo) for HTML output

## Output Configuration

The project is configured to output to both HTML (with cosmo theme) and PDF (using scrbook document class with custom geometry for 6"x9" format). The HTML version includes search functionality and download links for PDF/EPUB formats.