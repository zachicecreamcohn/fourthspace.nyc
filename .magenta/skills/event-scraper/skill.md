---
name: event-scraper
description: Scrape and filter events from a URL for Fourth Space NYC — a curated NYC events site for artists, technologists, theatre makers, and curious New Yorkers. Use this skill when the user provides a URL and wants to find relevant events, filter events from a site, or populate the research/ folder with event data. Also use it when the user asks to "research events", "scrape events", or "find things to add to the site".
---

# Event Scraper

Given a URL (events listing page) and an optional date range, fetch the page, evaluate each event against Fourth Space's editorial criteria, and write the relevant ones to a timestamped JSON file in `research/`.

## Who Fourth Space is for

Fourth Space (fourthspace.nyc) surfaces free or cheap NYC events for people who find joy at the intersection of **arts, technology, performance, and intellectual culture**. The audience includes:

- Software engineers, makers, hackers, and technologists
- Artists, theatre makers, musicians, lighting/video designers, and other creative practitioners
- People drawn to intelligent comedy, niche performance, and cerebral entertainment
- Curious, culturally engaged New Yorkers who appreciate the weird, the nerdy, and the classically NYC

An event doesn't need to be at the *intersection* of tech and art — it just needs to appeal to at least one of these groups.

## Relevance criteria

**Include** an event if it fits any of these:
- Technology + art crossover (generative art, live coding, interactive installations, DIY electronics, creative coding, projection/lighting design)
- Theatre, experimental performance, immersive experience, or dance — especially downtown/indie/fringe
- Music with an interesting angle: experimental, electronic, classical, jazz, avant-garde, or a unique venue/context
- Intelligent or nerdy comedy (e.g. science comedy, improv for nerds, storytelling like The Moth)
- Talks, panels, or lectures that are genuinely intellectual or culturally stimulating (not corporate)
- Film screenings with a curatorial angle (retrospectives, experimental, themed series)
- Maker/craft events or hands-on workshops
- Classically "only in New York" events — quirky, neighborhood-rooted, culturally specific
- Free or cheap (strongly preferred; tickets under ~$25 unless the event is exceptional)

**Exclude** an event if it is:
- Mainstream commercial concerts or Broadway at full price
- Purely athletic or fitness-focused
- Standard nightlife (bar nights, club events) with no arts/intellectual angle
- Overly corporate, startup-y, or tech-bro-focused (pitch competitions, "networking for founders", AI product launches)
- Focused primarily on AI as a business/hype topic
- Very expensive with nothing exceptional to justify it

When in doubt, include it — the human curator can filter further.

## Steps

1. Fetch the URL. Try `mcp_fetch_fetch` first. If the page requires JavaScript to render (e.g. a React/SPA site), fall back to the Playwright MCP (`mcp_playwright_browser_navigate` + `mcp_playwright_browser_snapshot` or `mcp_playwright_browser_evaluate`).
2. If the page is paginated or links to individual event pages, follow links as needed to gather full event details (title, description, date, price, location).
3. Evaluate each event against the criteria above.
4. Collect all **relevant** events into a JSON array (see output format).
5. Write results to `research/<YYYY-MM-DD>-<slug>.json` where `<slug>` is a short identifier derived from the source URL (e.g. `bam`, `eventbrite`, `brooklynrail`).

## Output format

```json
{
  "source_url": "https://...",
  "scraped_at": "YYYY-MM-DD",
  "date_range": "e.g. June 2026 (omit if not specified)",
  "events": [
    {
      "title": "Event title",
      "description": "1–2 sentence description of what the event is",
      "date": "YYYY-MM-DD or human-readable if exact date unknown",
      "price": "Free / $10 / $5–$15 / etc.",
      "location": "Venue name, neighborhood or borough",
      "url": "Direct link to event page if available",
      "tags": ["tag1", "tag2"],
      "relevance_reason": "One sentence explaining why this fits Fourth Space"
    }
  ]
}
```

## Tags

Use lowercase tags drawn from (but not limited to):
`art`, `music`, `theatre`, `performance`, `tech`, `interactive`, `film`, `comedy`, `talk`, `lecture`, `workshop`, `maker`, `experimental`, `free`, `paid`, `dance`, `immersive`, `nyc-native`, `outdoor`, `brooklyn`, `manhattan`, `queens` etc etc

## Date range filtering

If the user specifies a date range (e.g. "events in June" or "this weekend"), only include events within that range. If no range is given, include all upcoming events found.
