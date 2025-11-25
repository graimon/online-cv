# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal online CV/resume website built with **Jekyll**, a static site generator. It uses the [Online CV Jekyll Theme](http://webjeda.com/online-cv/) and is deployed as a static site on GitHub Pages.

**Key Features:**
- Multi-language support (English and Spanish) via `jekyll-multiple-languages-plugin`
- Multiple color scheme styles (6 available)
- PDF export capability via `jekyll-pdf`
- Responsive design
- Asset pipeline with `jekyll-assets`

## Development Setup

### Prerequisites
- Ruby (with `bundle`)
- Jekyll 3.8.5+

### Common Commands

**Install dependencies:**
```bash
bundle install
```

**Start local development server:**
```bash
bundle exec jekyll serve
```
The site will be available at `http://localhost:4000`

**Build for production:**
```bash
bundle exec jekyll build
```
Output goes to `_site/` directory.

**Clean build artifacts:**
```bash
bundle exec jekyll clean
```

## Project Structure

### Core Configuration
- `_config.yml` - Main Jekyll configuration and site metadata (name, email, social links, style selection)
- `Gemfile` / `Gemfile.lock` - Ruby dependencies
- `.gitignore` - Excludes `_site/`, `.sass-cache/`, `.jekyll-metadata`, IDE files

### Content & Translations
- `_i18n/` - Language YAML files (`en.yml`, `es.yml`)
  - All content strings are defined here (career, experiences, education, skills, projects, languages, interests)
  - The plugin uses `{% t key.path %}` Liquid tags to insert translated content
  - Language switching is handled via `/` (Spanish) and `/en/` URLs

### Templates & Layouts
- `_layouts/default.html` - Main page layout (sidebar + main content wrapper)
- `_layouts/compress.html` - HTML minification layout (extended by default.html)
- `_layouts/pdf.html` - PDF export layout for jekyll-pdf plugin
- `_includes/` - Reusable template components:
  - `head.html` - Meta tags, stylesheets, fonts
  - `sidebar.html` - Profile picture, contact info, language toggle
  - `career-profile.html` - Career overview section
  - `experience.html` - Work experience entries (references `_i18n` data)
  - `education.html` - Education section
  - `skills.html` - Technical skills display
  - `projects.html` - Open source projects
  - `interests.html` - Personal interests
  - `language.html` - Language proficiencies
  - `footer.html` - Footer content
  - `scripts.html` - JavaScript includes

### Assets
- `assets/` - CSS, JavaScript, images, and third-party libraries (Bootstrap, FontAwesome)
- `assets/images/` - Profile picture (`profile.jpg`) and theme images

### Entry Point
- `index.html` - Root page (uses default layout, content filled via includes)

## Key Concepts

### Multi-Language System
The `jekyll-multiple-languages-plugin` enables language switching:
- Set active language in `_config.yml` via `languages:` array and default via `exclude_from_localizations`
- Use `{% t key.path %}` in templates to reference strings from `_i18n/*.yml`
- Language-specific URLs: `/` for default (Spanish), `/en/` for English
- Language selector in `_includes/sidebar.html` checks `site.lang` to toggle between languages

### Style Customization
Edit `_config.yml` to enable different color schemes (uncomment one):
```yaml
#style: styles-2
#style: styles-3
#style: styles-4
#style: styles-5
style: styles-6  # Currently active
```

### Content Editing
All CV content is managed in `_i18n/*.yml` files:
- Edit `_i18n/en.yml` for English content
- Edit `_i18n/es.yml` for Spanish content
- Site metadata (name, email, links) lives in `_config.yml`
- Includes reference content via Liquid tags; changes to YAML automatically reflect on the site

## Build Output

- **Development server:** `http://localhost:4000` (hot-reload on file changes)
- **Production build:** Outputs to `_site/` (git-ignored)
- **GitHub Pages:** Deploy `gh-pages` branch for automatic publishing

## Deployment to GitHub Pages

Deployment is **fully automated** via GitHub Actions. Simply:

1. **Make changes and push to master:**
```bash
git add .
git commit -m "Your changes"
git push origin master
```

2. **GitHub Actions automatically:**
   - Builds the Jekyll site (with `bundle exec jekyll build`)
   - Uploads the `_site/` artifacts
   - Deploys to GitHub Pages

The site will be live at your GitHub Pages URL within seconds of pushing to master. Monitor the workflow status in the **Actions** tab on GitHub.

**Manual build for local testing:**
If you want to build locally before pushing:
```bash
bundle exec jekyll build    # Generates _site/
bundle exec jekyll serve    # Local preview at http://localhost:4000
```

## Dependencies

- `jekyll` (~> 4.3) - Static site generator (modern version for compatibility with Ruby 3.0+)
- `jekyll-multiple-languages-plugin` (~> 1.5) - Multi-language support
- `pry` - Ruby debugging (development)

**Gems removed** (due to compatibility issues):
- ~~`jekyll-assets`~~ - Not compatible with Jekyll 4.x; use alternative static asset solutions if needed
- ~~`jekyll-pdf`~~ - Upstream fork missing commit; use external PDF generation if needed

## GitHub Actions Deployment

A GitHub Actions workflow is configured in `.github/workflows/pages.yml` that automatically:
- Builds the Jekyll site on push to master
- Uploads artifacts to GitHub Pages
- Deploys the built site to GitHub Pages

This workflow handles all deployment automatically—just push to master and the site builds and deploys.

## Notes for Future Development

- The theme is based on a 3rd Wave Media design; modifications should preserve responsive behavior
- When adding new CV sections, add entries to `_i18n/*.yml` and create corresponding includes in `_includes/`
- The site uses Liquid templating extensively; be familiar with `{% include %}`, `{% t %}`, and conditional tags
- Assets are referenced in `_includes/head.html` and `_includes/scripts.html`
- Color themes are CSS-based; switch via `style` config or add new theme files in `assets/`
