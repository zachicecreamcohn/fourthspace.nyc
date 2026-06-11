# fourthspace.nyc — Claude Context

A Hugo static site for weekly curated NYC events for techy creatives and artists. Deployed to [fourthspace.nyc](https://fourthspace.nyc) via GitHub Actions.

## Stack

- Hugo static site generator
- Theme: customized [smol](https://github.com/colorchestra/smol) (monospaced base, heavily modified)
- Font: Mozilla Text (Google Fonts)
- Deployed via `.github/workflows/deploy.yml` → GitHub Pages

## Commands

```bash
# Start dev server
hugo server

# Create a new post
hugo new content posts/2026-06-13.md
```

## Content

Posts live in `content/posts/` named by date (e.g. `2026-06-10.md`).

Each post is a weekly issue containing a list of events.

### Frontmatter

```yaml
---
title: "Issue #1 — Jun 13"
date: 2026-06-13T00:00:00-04:00
type: posts
draft: false
tags:
  - music
  - tech
---
```

### Preview truncation

Place `<!--more-->` in the body to control where the summary cuts off on the index/list page. Everything before it is shown as the preview.

```markdown
Short teaser paragraph.

<!--more-->

Rest of the post...
```

### Subway line badges (`{{< trains >}}` shortcode)

Use the `trains` shortcode inline in post body to show MTA subway line badges next to an event. Pass line letters/numbers as quoted arguments.

```markdown
## Jazz Night at Pioneer Works
{{< trains "A" "C" "F" >}}
Friday June 13, 7pm · Free · Red Hook, Brooklyn
```

Supported lines: `1 2 3 4 5 6 7 A B C D E F G J L M N Q R S W Z`

Badge colors match official MTA colors. The `N Q R W` badges use black text (yellow background).

## Layout files

- `layouts/partials/header.html` — site header with nameplate + subtitle
- `layouts/_default/single.html` — single post view
- `layouts/_default/summary.html` — post preview card
- `layouts/_default/list.html` — post list (index, tags, etc.)
- `layouts/shortcodes/trains.html` — MTA badge shortcode

## Styles

`static/css/style.css` — all styles. Uses CSS variables for light/dark mode:

- `--bgcolor`, `--fontcolor` — background and text
- `--linkcolor`, `--visitedcolor` — link colors (navy blue / steel blue)
- `--precolor`, `--prebgcolor` — code blocks

## Config (`hugo.toml`)

```toml
baseURL = 'https://fourthspace.nyc/'
title = 'fourthspace.nyc'

[params]
subtitle = "Free and cheap NYC events for techy creatives and artists."
dateFmt = "Jan 2, 2006"
copyright = "Fourth Space NYC"
```
