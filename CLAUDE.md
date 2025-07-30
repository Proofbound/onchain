# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a multi-language Quarto book project with the following titles:
- **English**: "Onchain Commerce Unveiled: Engineering the Next Era of Digital Trade" by Apollo Sun
- **Simplified Chinese**: "链上商业崛起：第三次商业革命指南" by 孫波 (Apollo Sun) 著
- **Traditional Chinese**: "鏈上商業崛起：第三次商業革命指南" by 孫波 (Apollo Sun) 著

The project uses the Quarto publishing system to generate HTML and PDF versions of the book from Markdown source files in three languages.

## Architecture

### Main Structure
- **Root Configuration**: `_quarto.yml` defines the main website structure with language selection
- **Language Directories**: 
  - `en/` - English version with its own `_quarto.yml` and content files
  - `zh/` - Simplified Chinese version 
  - `zh-tw/` - Traditional Chinese version
- **Assets**: `assets/` directory contains shared images, CSS, and other resources
- **Output**: `docs/` directory contains generated files for GitHub Pages

### Content Files
- `.qmd` files contain book chapters and content
- Each language has its own set of chapter files
- Main chapters: CH01 through CH14, plus index, intro, references
- Bibliography: `references.bib` for citations

### Asset Management
- **Images**: Located in `assets/images/` (e.g., `Ch3-6-pillars.jpg`, `ch2-overview.jpg`)
- **CSS**: Custom styling in `assets/css/custom.css`
- **Cover**: `assets/crypto-cover1.jpg` used across all language versions

## Development Commands

### Building Individual Language Versions
```bash
# English version
cd en/ && quarto render --to html

# Simplified Chinese version  
cd zh/ && quarto render --to html

# Traditional Chinese version
cd zh-tw/ && quarto render --to html
```

### Building All Versions
```bash
# Build and deploy all language versions
cd en/ && quarto render --to html
cd ../zh/ && quarto render --to html
cd ../zh-tw/ && quarto render --to html

# Copy to main docs directory
cp -r en/docs/* docs/en/
cp -r zh/docs/* docs/zh/
cp -r zh-tw/docs/* docs/zh-tw/
```

### Main Language Selection Page
```bash
# Render the main language selection page
quarto render index.qmd --to html
```

### Publishing
```bash
# Publish to GitHub Pages (configured for proofbound.github.io/crypto-jason/)
quarto publish gh-pages
```

## File Structure

```
/
├── _quarto.yml                 # Main website configuration
├── index.qmd                   # Language selection page
├── assets/                     # Shared assets
│   ├── css/custom.css         # Custom styling
│   ├── images/                # Book diagrams and illustrations
│   └── crypto-cover1.jpg      # Book cover image
├── en/                        # English version
│   ├── _quarto.yml           # English book configuration
│   ├── index.qmd             # English preface
│   ├── intro.qmd             # English introduction
│   ├── CH01-*.qmd            # English chapters
│   └── docs/                 # Generated English HTML
├── zh/                       # Simplified Chinese version
│   ├── _quarto.yml          # Chinese book configuration
│   ├── index.qmd            # Chinese preface
│   ├── intro.qmd            # Chinese introduction
│   ├── CH01-*.zh.qmd        # Chinese chapters
│   └── docs/                # Generated Chinese HTML
├── zh-tw/                   # Traditional Chinese version
│   ├── _quarto.yml         # Traditional Chinese configuration
│   ├── index.qmd           # Traditional Chinese preface  
│   ├── intro.qmd           # Traditional Chinese introduction
│   ├── CH01-*.zh.qmd       # Traditional Chinese chapters
│   └── docs/               # Generated Traditional Chinese HTML
└── docs/                   # Main output for GitHub Pages
    ├── index.html         # Language selection page
    ├── en/               # English book files
    ├── zh/               # Simplified Chinese book files
    └── zh-tw/            # Traditional Chinese book files
```

## Content Editing

### Language-Specific Content
- Each language version has its own complete set of `.qmd` files
- Content should be properly localized, not just translated
- Traditional Chinese uses proper character variants distinct from Simplified Chinese
- Chinese versions follow publishing conventions (author names include 著 character)

### Image References
- All images should reference `/assets/images/` paths
- **IMPORTANT**: Never use `/_resources/` paths (GitHub Pages ignores underscore directories)
- Example: `![Six Pillars](/assets/images/Ch3-6-pillars.jpg)`

### Supported Features
- Cross-references between chapters
- Bibliography citations using BibTeX
- PDF and HTML output formats
- CJK font support for Chinese characters
- Bootstrap theme (cosmo) for HTML output
- Multi-language navigation and search

## Output Configuration

### HTML Output
- Uses cosmo Bootstrap theme
- Includes search functionality
- Download links for PDF/EPUB formats
- Responsive design with sidebar navigation

### PDF Output  
- Uses scrbook document class
- Custom 6"x9" page geometry
- XeLaTeX engine for CJK character support
- Proper font configuration for Chinese text

### GitHub Pages Deployment
- Main site serves language selection page
- Each language version deployed to subdirectory (`/en/`, `/zh/`, `/zh-tw/`)
- All assets served from `/assets/` directory (no underscore prefixes)

## Important Notes

### Asset Paths
- Always use `assets/` not `_resources/` for asset paths
- GitHub Pages ignores directories starting with underscore
- Images should be referenced as `/assets/images/filename.jpg`

### Chinese Publishing Conventions
- Chinese author names must include 著 character: "孫波 (Apollo Sun) 著"
- Use proper Traditional vs Simplified Chinese character variants
- Maintain consistent terminology across Chinese versions

### Rendering Workflow
1. Make changes to source `.qmd` files
2. Render each language version independently from its directory
3. Copy generated `docs/` contents to main `docs/` directory structure
4. Commit and push to update GitHub Pages

### Multi-language Management
- Keep terminology consistent across language versions
- Ensure chapter structures match between languages
- Update all language versions when making structural changes
- Test rendering of all languages before deployment