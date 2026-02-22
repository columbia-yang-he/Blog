---
title: "Quick setup workflow for my Weather MCP demo"
description: "The shortest reliable path from API key to a working Claude-connected weather tool."
pubDate: "2026-02-14"
tags: ["setup", "mcp", "developer-workflow"]
---

I wrote this setup process to optimize for speed and low friction.

If you want to get a weather MCP server running quickly, this is the path I use.

## Setup sequence

1. Create an OpenWeatherMap account and generate an API key.
2. Copy `.env.example` to `.env`.
3. Set `OPENWEATHER_API_KEY` in `.env`.
4. Install dependencies and build.
5. Add the server entry to Claude Code MCP settings.
6. Restart Claude Code and test with a weather prompt.

## Why this order works

It catches activation and configuration issues early:

- API key problems show up before host integration.
- Build failures are separated from runtime configuration.
- Tool wiring is tested only after local validation.

## Common troubleshooting shortcuts

- `401 Unauthorized`: key not active yet or copied incorrectly.
- `404 City Not Found`: city spelling or format issue.
- Server not loading: check build output and MCP settings path.

## Recommended validation prompts

I usually run:

- "What's the weather in Tokyo?"
- "Give me a 5-day forecast for Berlin."
- "Compare weather in London and New York."

These quickly verify both tools and basic argument handling.

## Next steps after basic setup

Once it works end-to-end, the most valuable upgrades are:

- better logging,
- smarter caching,
- and additional weather tools such as UV or air quality.
