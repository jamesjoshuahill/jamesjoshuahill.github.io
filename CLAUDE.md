# Personal Website - Built with Claude Code

## Overview

Personal career website for Josh Hill, showcasing a career in software engineering across fintech, cloud platforms, education, and renewable energy. The site emphasizes a human-centered approach to technology and collaboration.

**Live site:** https://jamesjoshuahill.github.io/

## Technology Stack

- **Hugo** 0.152.2 - Static site generator (chosen because Go is the main programming language)
- **GitHub Actions** - Automated deployment pipeline
- **GitHub Pages** - Hosting

## Design

### Style Approach
- Minimal resume page with warm, approachable design
- Distinctively warm color palette and friendly typography
- Human-centered storytelling focused on career milestones

### Color Palette (Warm Earth Tones)
- Background: `#FAF7F2` (warm cream)
- Primary text: `#3E2723` (rich brown)
- Accent/links: `#D97757` (terracotta)
- Secondary text: `#6B4E3D`, `#8B7355` (warm browns)
- Card background: `#FFFFFF` (white)
- Borders/underlines: `#F4E8DB` (peach)

### Typography
- **Headings (H1, H2, H3):** Bitter (serif) - gives gravitas and warm character
- **Body text:** Work Sans (sans-serif) - clean and easy to read
- Traditional pairing approach for professional yet warm feel

### Layout
- Card-based sections with rounded corners (12-16px border radius)
- Soft shadows for depth
- Profile photo with terracotta border
- Mobile-responsive design

## Content Structure

1. **Header** - Name, title, location (Remote, UK), GitHub link, profile photo
2. **About Me** - Human-centered philosophy and career overview
3. **Current Role** - Arenko (grid-scale battery management)
4. **Career Journey**
   - Enabling Payment Systems at Scale (Form3)
   - Coaching Career Changers (Makers)
   - Building Cloud Platforms (Pivotal, CloudCredo)
5. **What I Bring** - Key strengths and technical depth

## Development

### Local Development
```bash
# Start development server
hugo server --buildDrafts --bind 0.0.0.0

# Visit http://localhost:1313/
```

### File Structure
- `hugo.toml` - Site configuration
- `content/_index.md` - Homepage content (markdown with HTML for layout)
- `layouts/index.html` - Homepage template with embedded CSS
- `.github/workflows/deploy.yml` - GitHub Actions deployment workflow
- `.gitignore` - Excludes build artifacts (`public/`, `.hugo_build.lock`)

### Making Changes
1. Edit content in `content/_index.md`
2. Edit design in `layouts/index.html`
3. Test locally with `hugo server`
4. Commit and push to master branch
5. GitHub Actions automatically builds and deploys

## Deployment

Automated via GitHub Actions on every push to master:
1. Installs Hugo CLI
2. Builds site with `hugo --gc --minify`
3. Uploads build artifact
4. Deploys to GitHub Pages

**GitHub Pages Settings:**
- Source: GitHub Actions
- Custom domain: None
- HTTPS: Enforced

## Design Decisions

- **No redundancy mentions** - Removed references to being made redundant from Form3 and Makers
- **No dating industry** - Removed Venntro and all dating platform references
- **No CloudCredo link** - Company no longer exists, kept as text only
- **Company links** - All active companies have links to their websites
- **Location added** - "Remote, UK" for context
- **Section rename** - "Coaching Career Changers" better describes the Makers experience

## Future Enhancements

Potential additions:
- Blog section for technical writing
- Projects showcase
- Speaking engagements/talks page
- Contact form
- RSS feed

---

Built with Claude Code on 2025-11-08
