# fourthspace.nyc — Claude Context

A Hugo static site for weekly curated NYC events for techy creatives and artists. Deployed to [fourthspace.nyc](https://fourthspace.nyc) via GitHub Actions.

## Stack

- Hugo static site generator
- Theme: customized [smol](https://github.com/colorchestra/smol) (monospaced base, heavily modified)
- Font: Mozilla Text (Google Fonts)
- Deployed via `.github/workflows/deploy.yml` → GitHub Pages

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

Badge rendering lives in the `layouts/partials/trains.html` partial. Both the `trains` shortcode and the `event` shortcode call it, so it's the single source of truth.

### Event listings (`{{< event >}}` shortcode)

Use the `event` shortcode to render a single event card. Events are grouped under `##` day-of-week headings within a post. Separate adjacent events with a blank line.

```markdown
{{< event
  title="Rouge Salon: Absurd True Tales"
  price="$24 ($25 at the door)"
  org="Caveat"
  trains="F J M Z"
  free="true"
  url="https://www.caveat.nyc/events/..."
>}}
Description in markdown (rendered as the card body).
{{< /event >}}
```

Params:
- `title` — event name (required)
- `price` — cost text
- `org` — hosting venue/organization (short, e.g. "Caveat")
- `trains` — space-separated MTA lines; rendered as badges pushed to the right of the title
- `url` — optional; links the title
- `free` — optional boolean (`"true"`); prefixes the price with a green `FREE` badge

Do not include a full address — just the `org` plus nearby `trains` (look up the nearest station for the venue).

## Layout files

- `layouts/partials/header.html` — site header with nameplate + subtitle
- `layouts/_default/single.html` — single post view
- `layouts/_default/summary.html` — post preview card
- `layouts/_default/list.html` — post list (index, tags, etc.)
- `layouts/shortcodes/trains.html` — MTA badge shortcode
- `layouts/shortcodes/event.html` — event card shortcode
- `layouts/partials/trains.html` — shared MTA badge rendering (used by both shortcodes)

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
