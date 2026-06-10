# Fourth Space NYC

A curated weekly guide to free and cheap NYC events for techy creatives and artists — built with Hugo and the [smol](https://github.com/colorchestra/smol) theme.

> "One of the best parts of this city is that, although the rent is high, there are practically infinite free (or very cheap) activities and events for every niche."

## About

Fourth Space NYC is a personal project by Zach, a software engineer and lighting/video designer for theatre. The goal is a curated list of activities and events for geeky people who find joy at the intersection of arts and technology.

The site is deployed to [fourthspace.nyc](https://fourthspace.nyc) via GitHub Actions → GitHub Pages.

## Stack

- [Hugo](https://gohugo.io/) static site generator
- [smol](https://github.com/colorchestra/smol) theme (monospaced, no JS, no trackers)
- GitHub Actions for CI/CD

## Development

```bash
hugo server
```

The site will be available at `http://localhost:1313`.

## Deployment

Pushes to `main` automatically build and deploy via `.github/workflows/deploy.yml`.

In your GitHub repo settings, go to **Settings → Pages → Source** and set it to **GitHub Actions**.

## Config

Key settings in `hugo.toml`:

```toml
baseURL = 'https://fourthspace.nyc/'
title = 'Fourth Space NYC'

[params]
subtitle = "Free and cheap NYC events for techy creatives and artists."
dateFmt = "Jan 2, 2006"
copyright = "Fourth Space NYC"
```

## License

Content © Fourth Space NYC. Theme ([smol](https://github.com/colorchestra/smol)) released under the [MIT license](https://github.com/colorchestra/smol/blob/master/LICENSE).
