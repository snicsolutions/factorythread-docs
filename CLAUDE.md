# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Jekyll-based documentation site for Factory Thread, built with the Just the Docs theme and deployed to GitHub Pages. The site is hosted at https://snicsolutions.github.io/factorythread-docs/.

## Development Commands

### Local Development
```bash
# Install dependencies
bundle install

# Start local development server
bundle exec jekyll serve

# Local site will be available at http://localhost:4000/factorythread-docs
```

### Content Creation
```bash
# Add new documentation page in docs/ directory with front matter:
---
layout: default
title: Your Page Title
nav_order: 5
---
```

## Architecture

### Site Structure
- `_config.yml` - Main Jekyll configuration with Just the Docs theme settings
- `index.md` - Homepage with Factory Thread branding and navigation
- `docs/` - Documentation pages (getting-started.md, features.md, api-reference.md)
- `images/` - Logo and favicon assets
- `.github/workflows/pages.yml` - Automated GitHub Pages deployment

### Key Configuration
- Uses `just-the-docs` theme with dark color scheme
- Search functionality enabled
- GitHub edit links configured to point to `docs/` source
- Auto-deployment via GitHub Actions on pushes to main branch
- Logo and favicon configured in `/images/` directory

### Navigation
- Homepage (`nav_order: 1`)
- Getting Started (`nav_order: 2`) 
- Features (`nav_order: 3`)
- API Reference (`nav_order: 4`)

## Deployment

The site auto-deploys via GitHub Actions when changes are pushed to the main branch. The workflow:
1. Builds Jekyll site with Ruby 3.1
2. Uses bundler cache for faster builds
3. Deploys to GitHub Pages with proper baseurl handling

## Important Notes

- All documentation pages must use `layout: default`
- Avoid Jekyll liquid tag links to non-existent files (causes build failures)
- Logo path is `/images/ft-logo.png`, favicon is `/images/favicon.ico`
- GitHub repository links should point to `snicsolutions/factorythread-docs`
- Site baseurl is `/factorythread-docs` for GitHub Pages deployment