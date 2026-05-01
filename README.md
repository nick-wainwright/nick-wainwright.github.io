# Technical Governance Portfolio

A Jekyll blog for a Governance, Computer Science & Cybersecurity portfolio, designed for GitHub Pages.

## Quick Start

### Prerequisites
- Ruby 3.x
- Bundler (`gem install bundler`)

### Local Development

```bash
git clone https://github.com/yourusername/yourusername.github.io
cd yourusername.github.io
bundle install
bundle exec jekyll serve --livereload
```

Then open `http://localhost:4000`.

---

## Deployment to GitHub Pages

1. Create a repo named `yourusername.github.io`
2. Push this repo to `main` branch
3. Go to **Settings → Pages → Source** → select **GitHub Actions**
4. The included workflow (`.github/workflows/deploy.yml`) handles the build and deploy automatically

---

## Customization

### `_config.yml`
Update these fields first:
```yaml
title: "Your Name"
description: "Your tagline"
author: "Your Name"
email: "you@email.com"
url: "https://yourusername.github.io"
linkedin: "https://linkedin.com/in/yourprofile"
github: "https://github.com/yourusername"
orcid: "https://orcid.org/0000-0000-0000-0000"
```

### Adding Blog Posts
Create files in `_posts/` with the naming convention `YYYY-MM-DD-title.md`:

```yaml
---
layout: post
title: "Your Post Title"
date: 2024-11-01
post_type: "White Paper"   # White Paper | Case Study | Blog Post | Research
read_time: 8               # estimated minutes
excerpt: "Short description shown in listings."
---

Your content here in Markdown.
```

### Adding Projects
Create files in `_projects/`:

```yaml
---
layout: project
title: "Project Name"
date: 2024-01-01
description: "One-line description for the card."
tags: [Python, Security, Compliance]
github: "https://github.com/you/repo"   # optional
---

Project details in Markdown.
```

### Contact Form
The contact page uses [Formspree](https://formspree.io) (free tier available).
1. Create a free Formspree account
2. Create a form and get your form ID
3. Replace `YOUR_FORM_ID` in `contact.html`:
   ```html
   <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```

### Resume
Drop your PDF resume at `assets/resume.pdf` — the nav button links there automatically.

---

## File Structure

```
.
├── _config.yml          # Site configuration
├── _layouts/
│   ├── default.html     # Base layout (nav + footer)
│   ├── post.html        # Blog post layout
│   └── project.html     # Project case study layout
├── _includes/
│   ├── nav.html         # Navigation
│   └── footer.html      # Footer
├── _posts/              # Blog posts (YYYY-MM-DD-slug.md)
├── _projects/           # Project case studies
├── assets/
│   ├── css/main.scss    # All styles
│   └── resume.pdf       # Your resume (add manually)
├── index.html           # Homepage
├── blog.html            # Blog listing
├── projects.html        # Projects listing
├── about.html           # About page
├── contact.html         # Contact page
├── Gemfile
└── .github/workflows/deploy.yml
```
