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
- **Centralized Assets**: All assets stored in `/assets/` directory organized by type
  - `/assets/covers/` - Book covers with language suffixes (crypto-cover1.jpg, crypto-jason-cover-zh-tw.pdf)
  - `/assets/docs/` - Documentation files (PDFs, instructions)
  - `/assets/images/` - Diagrams, logos, CSS files (Ch3-6-pillars.jpg, ch2-overview.jpg, Ch9-F2C-System.jpg)
- **Asset Symlinks**: Each language directory (`en/`, `zh/`, `zh-tw/`) has symlink to `../assets` for PDF rendering
- **Deployment**: Assets copied to `/docs/assets/` and language-specific `/docs/{lang}/assets/` during build

## Development Commands

### Complete Build and Deployment Process
**IMPORTANT**: Always follow this exact sequence to ensure all assets are properly deployed:

```bash
# 1. Render main language selection page
quarto render index.qmd --to html

# 2. Render all language versions (HTML + PDF)
cd en/ && quarto render --to html && quarto render --to pdf
cd ../zh/ && quarto render --to html && quarto render --to pdf  
cd ../zh-tw/ && quarto render --to html && quarto render --to pdf

# 3. Copy all rendered files to main docs structure
cp -r en/docs/* docs/en/
cp -r zh/docs/* docs/zh/
cp -r zh-tw/docs/* docs/zh-tw/

# 4. Ensure all assets are copied to deployment directories
cp -r assets/images/* docs/assets/images/
cp -r assets/images/* docs/en/assets/images/
cp -r assets/images/* docs/zh/assets/images/
cp -r assets/images/* docs/zh-tw/assets/images/

# 5. Commit and push to GitHub
git add -A
git commit -m "Update all language versions and assets"
git push
```

### Individual Language Rendering
```bash
# English version (HTML + PDF)
cd en/ && quarto render --to html && quarto render --to pdf

# Simplified Chinese version (HTML + PDF)
cd zh/ && quarto render --to html && quarto render --to pdf

# Traditional Chinese version (HTML + PDF)
cd zh-tw/ && quarto render --to html && quarto render --to pdf
```

### Asset Management Commands
```bash
# Verify asset symlinks exist (required for PDF rendering)
ls -la en/assets zh/assets zh-tw/assets

# Create missing symlinks if needed
cd en/ && ln -sf ../assets .
cd ../zh/ && ln -sf ../assets .
cd ../zh-tw/ && ln -sf ../assets .

# Check deployed assets match source
diff -r assets/images docs/assets/images
```

## File Structure

```
/
├── _quarto.yml                 # Main website configuration
├── index.qmd                   # Language selection page
├── assets/                     # Centralized assets (version controlled)
│   ├── covers/                # Book covers with language suffixes
│   │   ├── crypto-cover1.jpg
│   │   ├── crypto-jason-cover-zh-tw.pdf
│   │   └── crypto-jason-cover-full.pdf
│   ├── docs/                  # Documentation files
│   │   ├── OnChainCommercer（初版).pdf
│   │   └── PAPERBACK_6.000x9.000_204_BW_WHITE_en_US.pdf
│   └── images/                # Diagrams, logos, CSS
│       ├── Ch3-6-pillars.jpg
│       ├── ch2-overview.jpg
│       ├── Ch9-F2C-System.jpg
│       ├── Ch9-F2C-USDC-Wallet.jpg
│       ├── css/custom.css
│       └── proofbound-logo-*.svg
├── en/                        # English version
│   ├── _quarto.yml           # English book configuration
│   ├── assets -> ../assets   # Symlink for PDF rendering
│   ├── index.qmd             # English preface
│   ├── CH01-*.qmd            # English chapters
│   └── docs/                 # Generated English HTML + PDF
├── zh/                       # Simplified Chinese version
│   ├── _quarto.yml          # Chinese book configuration
│   ├── assets -> ../assets   # Symlink for PDF rendering
│   ├── index.qmd            # Chinese preface
│   ├── CH01-*.zh.qmd        # Chinese chapters
│   └── docs/                # Generated Chinese HTML + PDF
├── zh-tw/                   # Traditional Chinese version
│   ├── _quarto.yml         # Traditional Chinese configuration
│   ├── assets -> ../assets   # Symlink for PDF rendering
│   ├── index.qmd           # Traditional Chinese preface  
│   ├── CH01-*.zh.qmd       # Traditional Chinese chapters
│   └── docs/               # Generated Traditional Chinese HTML + PDF
└── docs/                   # Main output for GitHub Pages
    ├── index.html         # Language selection page
    ├── assets/            # Deployed centralized assets
    │   ├── covers/
    │   └── images/
    ├── en/               # English book files + assets copy
    │   ├── *.html
    │   ├── Global-Business-Chain.pdf
    │   └── assets/
    ├── zh/               # Simplified Chinese book files + assets copy
    │   ├── *.html
    │   ├── 萬國商鏈.pdf
    │   └── assets/
    └── zh-tw/            # Traditional Chinese book files + assets copy
        ├── *.html
        ├── 萬國商鏈.pdf
        └── assets/
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
- Always use `/assets/images/filename.jpg` paths in content files (works for both HTML and PDF)
- **CRITICAL**: Never use `_resources/` paths (GitHub Pages ignores underscore directories)
- Cover images use `/assets/covers/filename.jpg` paths
- CSS references use `/assets/images/css/custom.css` path

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

## Troubleshooting

### Missing Images on GitHub Pages
**Problem**: Images display locally but not on GitHub Pages
**Solution**: 
1. Check if images exist in `/docs/assets/images/` and all `/docs/{lang}/assets/images/` directories
2. Run asset copying commands from deployment process above
3. Verify image filenames match exactly (case-sensitive)

### PDF Generation Fails
**Problem**: XeLaTeX cannot find images during PDF rendering
**Solution**:
1. Ensure asset symlinks exist: `ls -la en/assets zh/assets zh-tw/assets`
2. Create missing symlinks: `cd {lang}/ && ln -sf ../assets .`
3. Verify images use `/assets/images/` paths in content files

### Build Process Issues
**Problem**: Some files missing after deployment
**Solution**: Always follow the complete build process in exact order:
1. Main page → 2. All language versions → 3. Copy files → 4. Copy assets → 5. Commit

### Asset Management Best Practices
- **Single Source**: All assets in `/assets/` directory only
- **Version Control**: Assets directory is tracked by git (not in .gitignore)
- **Deployment**: Assets must be copied to all deployment directories
- **Verification**: Always check deployed assets match source before pushing