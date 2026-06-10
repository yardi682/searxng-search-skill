---
name: privacy-web-search
description: Search the web privately using a self-hosted SearXNG instance. Fetches and reads the full content of the top results and summarizes them. Use when the user asks to search the web, look something up online, find current information, or research any topic.
---

# Privacy Web Search (Self-hosted SearXNG)

## Overview
This skill searches the web privately via a self-hosted SearXNG instance, fetches the full content of the top results, and returns the text for you to summarize. No tracking, no third-party services.

## When to activate
Activate when the user asks to:
- Search the web or internet for anything
- Look up current news, events, or facts
- Research a topic online
- Find information that may be newer than your training data

## How to use

Call `run_js` with `index.html` and a JSON string containing:

- `query`: Required. The core search intent, concise and specific (e.g. "Sydney weather today", "best budget phone 2026")
- `num_results`: Optional. Number of results to fetch and read. Default 5, max 5.

### Example
```json
{
  "query": "fusion energy breakthroughs 2026",
  "num_results": 5
}
```

## Handling results

The tool returns a JSON object with a `result` field containing:
- `query`: the search query used
- `results`: array of objects, each with `title`, `url`, `snippet`, and `full_text`
- `source`: the search source used
- `instruction`: reminder to summarize

## After receiving results

1. Read the `full_text` field of each result carefully
2. Write a clear, coherent summary of **3-5 sentences** that directly answers the user's query
3. Highlight the most important and consistent findings across sources
4. Note any conflicting information between sources if relevant
5. End with a **Sources** list: each result's title and URL on its own line
6. If `full_text` says "(Could not fetch page content)" for a result, rely on its `snippet` instead
7. Keep the total response concise — the on-device context window is limited

## Important notes
- Never fabricate information — only summarize what the results contain
- If results seem outdated or off-topic, say so and suggest refining the query
- Some pages may block fetching — use the snippet as fallback for those
