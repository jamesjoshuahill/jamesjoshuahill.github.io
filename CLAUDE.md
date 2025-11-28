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
- **Font delivery:** Bunny Fonts CDN (privacy-friendly, GDPR-compliant alternative to Google Fonts)
- **Increased text sizes:** All text sizes increased for better readability (body: 1.125rem, headings scaled proportionally)

### Layout
- Card-based sections with rounded corners (12-16px border radius)
- Soft shadows for depth
- Profile photo with terracotta border
- Illustrated collaboration scenes (floating right on desktop, centered on mobile)
- Mobile-responsive design
- Dark mode support via `prefers-color-scheme`

## Content Structure

### Homepage
1. **Header** - Name, location (South coast, UK), email and GitHub link, profile photo
2. **Opening Statement** - Human-centered philosophy (three paragraphs with collaboration illustration)
3. **Career Journey**
   - Managing Grid-Scale Batteries (Arenko)
   - Enabling UK Payments at Scale (Form3)
   - Coaching Career Changers (Makers)
   - Building Cloud Platforms (Pivotal, CloudCredo)
4. **What I Enjoy** - Key strengths and technical depth

### Playbook
A section for practical guides and lessons learned from building and running software. Supports Mermaid diagrams for technical illustrations.

## Development

### Local Development
```bash
# Start development server
hugo server --buildDrafts --bind 0.0.0.0

# Visit http://localhost:1313/

# Create a new playbook post
hugo new playbook/my-post.md
```

### File Structure
```
.
├── .github/workflows/deploy.yml    # GitHub Actions deployment
├── .gitignore                      # Excludes public/, .hugo_build.lock
├── README.md                       # Brief greeting for visitors
├── CLAUDE.md                       # Design decisions (this file)
├── hugo.toml                       # Site configuration
├── archetypes/
│   └── default.md                  # Template for new posts
├── content/
│   ├── _index.md                   # Homepage content
│   └── playbook/
│       └── _index.md               # Playbook section index
├── layouts/
│   ├── index.html                  # Homepage (extends baseof.html)
│   ├── _default/
│   │   ├── baseof.html             # Base template with all CSS
│   │   ├── list.html               # Playbook listing
│   │   └── single.html             # Individual playbook post
│   └── shortcodes/
│       └── mermaid.html            # Mermaid diagram shortcode
└── static/
    ├── favicon.svg                 # Browser icon
    ├── remote_team_meeting.png     # Intro section illustration
    └── whiteboard_collaboration.png # Career section illustration
```

### Making Changes
1. Edit content in `content/_index.md` or `content/playbook/`
2. Edit design in `layouts/_default/baseof.html` (CSS is consolidated here)
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

- **Minimal header** - Removed "Software Engineer" tagline for cleaner presentation
- **Collaboration illustrations** - Warm-toned illustrated scenes to reinforce human-centered values (generated from real photos with Nana Banana)
- **Split paragraphs** - Opening statement and key sections broken into shorter paragraphs for better rhythm
- **No Oxford commas** - Consistent British English style throughout
- **No redundancy mentions** - Removed references to being made redundant from Form3 and Makers
- **No dating industry** - Removed Venntro and all dating platform references
- **No CloudCredo link** - Company no longer exists, kept as text only
- **Company links** - All active companies have links to their websites
- **Pivotal IPO mention** - Added concrete achievement (2018 IPO) to demonstrate platform value
- **Consolidated CSS** - All styles in baseof.html; homepage extends base template

## Future Enhancements

Potential additions:
- Projects showcase
- Speaking engagements/talks page
- Contact form
- RSS feed

---

Built with Claude Code on 2025-11-08
Updated 2025-11-11 - Added collaboration illustration and content refinements
Updated 2025-11-12 - Added README.md for public visitors
Updated 2025-11-13 - Switched to Bunny Fonts CDN and increased text sizes for better readability
Updated 2025-11-28 - Added playbook section with Mermaid diagram support
Updated 2025-11-28 - Consolidated CSS into baseof.html, updated documentation
