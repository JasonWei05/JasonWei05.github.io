# Personal Website

This is a minimal personal website built with Jekyll, designed for hosting on GitHub Pages.

## Features
- Clean, minimal design
- Blog section
- Paper Reviews section
- Markdown support for all content
- Tagging support for paper reviews
- Automatic Table of Contents support
- Social media links with icons (X, LinkedIn)

## How to Customize

### Social Links
Open `_config.yml` and update the `social_links` section with your profile URLs:
```yaml
social_links:
  x: https://x.com/yourhandle
  linkedin: https://linkedin.com/in/yourprofile
```

## How to Add Content

### Blog Posts
Add markdown files to the `_posts` directory with the format `YYYY-MM-DD-title.md`.
Front matter example:
```yaml
---
layout: post
title: "My Post Title"
date: 2023-10-27
---
```

### Paper Reviews
Add markdown files to the `_reviews` directory.
Front matter example:
```yaml
---
layout: post
title: "Review: Paper Title"
date: 2023-10-27
tags: [Transformers, NLP] # Add tags here
---

* Table of Contents
{:toc}

Your review content here...
```

## Deployment
Simply push this repository to GitHub. Go to Settings > Pages and ensure it's deploying from the root branch.
