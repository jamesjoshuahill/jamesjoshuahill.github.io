# Personal Website

Hi, I'm Josh Hill. This site describes my journey through software engineering across fintech, cloud platforms, education and renewable energy.

**Live site:** https://jamesjoshuahill.github.io/

Vibe-coded with Claude Code.

## Quick Start

```bash
# Install Hugo
brew install hugo

# Run locally
hugo server --buildDrafts --bind 0.0.0.0

# Visit http://localhost:1313/
```

## Stack

- Hugo 0.152.2 (static site generator)
- GitHub Actions (automated deployment)
- GitHub Pages (hosting)

## Design

This design features Bitter and Work Sans typefaces, warm earth tones and illustrations generated from real photos with Nana Banana in a responsive card-based layout.

## Structure

- `content/_index.md` - Homepage content
- `layouts/index.html` - Template with embedded CSS
- `static/` - Images and assets
- `.github/workflows/deploy.yml` - Deployment pipeline
- `CLAUDE.md` - Detailed documentation and design decisions
