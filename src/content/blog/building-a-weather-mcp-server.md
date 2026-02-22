---
title: "Building a Weather MCP Server with OpenWeatherMap"
description: "How I built a practical MCP server that gives Claude real-time weather and forecast data."
pubDate: "2026-02-16"
tags: ["mcp", "typescript", "api"]
---

I built a small MCP server to connect Claude with real weather data from OpenWeatherMap.

The goal was simple: when I ask a weather question, Claude should call tools that return live current conditions and a short forecast, not guessed text.

## What the server exposes

The server currently implements two tools:

- `get_weather` for current conditions in a city
- `get_forecast` for a 5-day forecast summary

Both tools are designed to be straightforward and production-friendly.

## Architecture at a glance

The request flow is:

1. User asks Claude for weather information.
2. Claude decides to call a tool.
3. The MCP server receives a JSON-RPC request over stdio.
4. The server calls OpenWeatherMap with the provided city.
5. The response is normalized and returned to Claude.

This keeps responsibilities clean: Claude handles reasoning and language, while the MCP server handles structured data access.

## Practical implementation notes

- Input parameters are validated before making API calls.
- API key handling stays in environment variables.
- Responses are cleaned up for readability (rounded values and unit conversion).
- Errors are translated into clear messages for common issues like invalid API keys or unknown cities.

## Why this project matters

This demo is small, but it captures the core MCP pattern:

- an LLM host,
- one focused tool server,
- one external API integration,
- and a stable protocol boundary.

That pattern scales well when adding more tools such as air quality, UV index, or weather alerts.
