---
title: "Weather MCP Architecture: JSON-RPC, stdio, and API boundaries"
description: "A practical architecture walkthrough of an MCP server from user prompt to external API response."
pubDate: "2026-02-15"
tags: ["architecture", "mcp", "json-rpc"]
---

One of the biggest benefits of MCP is that architecture stays explicit.

In this weather project, the data flow is transparent:

- Claude acts as the MCP host.
- My server acts as the MCP tool provider.
- OpenWeatherMap acts as the external data source.

## End-to-end flow

When a user asks for weather in a city:

1. Claude detects intent and chooses `get_weather`.
2. Claude sends a JSON-RPC `tools/call` request over stdio.
3. The server validates arguments and calls OpenWeatherMap.
4. The server transforms raw API fields into a concise response.
5. Claude uses that response to generate a natural-language answer.

The important point is each step has one clear responsibility.

## Protocol details that matter

Using JSON-RPC 2.0 over stdio gives three practical advantages:

- predictable request and response structure,
- stable IDs for matching responses,
- and a standard way to return errors.

This makes testing easier because requests can be reproduced exactly.

## Operational concerns

A few concerns become obvious early:

- free tier rate limits,
- malformed city inputs,
- unavailable network calls,
- and API key errors.

I handle these with explicit validation and user-readable error mapping instead of exposing raw upstream failures.

## What I would add next

If I extend this into a production tool, I would add:

- response caching to reduce API calls,
- richer observability,
- and optional unit systems per user preference.

Even as a demo, this architecture is a useful template for any MCP server that wraps a third-party API.
