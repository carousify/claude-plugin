# Carousify for Claude

Create, design, schedule and analyze LinkedIn and Instagram carousels and posts with [Carousify](https://carousify.com),
right from Claude.

![A LinkedIn carousel created by Claude with the Carousify plugin: cover, two content slides and the closing slide](assets/example-carousel.jpg)

*A carousel Claude wrote and designed through Carousify, rendered with the brand kit on every slide.*

## Install

In Claude Code:

```
/plugin install carousify --marketplace carousify/claude-plugin
```

## What it does

- **Write carousels** from a topic, notes, an article or a URL, using your Carousify templates or a brand-new design
  that Claude lays out for you (fonts, colors, icons and shapes from Carousify's library).
- **Stay on brand**: your brand kit's name, handle, logo, colors and fonts on every slide.
- **Post and schedule**: turn a carousel into a LinkedIn document post or an Instagram carousel, then schedule or
  publish it to your connected LinkedIn profiles, LinkedIn company pages and Instagram accounts. Anything public waits
  for your confirmation, and workspace roles and approval rules apply.
- **Use your own files**: upload images, videos or documents to use in posts.
- **Learn from analytics**: see how recent posts performed and get ideas for the next ones.

## What's included

- **Carousify connector** (remote MCP server at `https://api.carousify.com/mcp`). You sign in to Carousify and choose
  a workspace the first time Claude uses it (OAuth). No local install and no API key needed.
- **Carousify skill**: how to write carousels that get read (hooks, slide flow, length, calls to action), a library of
  design styles with example templates, brand kit rules and step-by-step workflows for posting, scheduling, uploads
  and analytics.
- **Commands**: `/carousify:carousel <topic>` creates a carousel draft; `/carousify:analytics` reviews recent posts.

## Requirements

A Carousify account with at least one connected LinkedIn or Instagram account. Some features (MCP access, scheduling
limits, workspace roles) depend on your Carousify plan.

## Data and privacy

This plugin runs no code on your computer. Claude talks only to Carousify's connector at `https://api.carousify.com`,
over HTTPS, with the access you grant when you sign in:

- It reads your workspace's connected accounts, posts, carousels, templates, brand kits and analytics.
- It creates and changes drafts, carousels and uploads in that workspace, and schedules, publishes or deletes posts
  when you ask (Claude shows you the final post and asks first).
- Posting to LinkedIn and Instagram happens from Carousify's servers through those networks' official APIs.

You can disconnect at any time from Claude's connector settings or in Carousify (Workspace settings › MCP). See the
[Carousify privacy policy](https://carousify.com/privacy-policy) for how Carousify stores and handles your data.

## Support

Email [hello@carousify.com](mailto:hello@carousify.com) or visit [carousify.com](https://carousify.com).

## License

MIT, see [LICENSE](LICENSE).
