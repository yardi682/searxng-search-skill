---
name: privacy-web-search
description: Search the web privately using SearXNG.
---

# Privacy Web Search (SearXNG)

## Overview
This skill lets you search the web privately via SearXNG — a free, open-source meta-search engine that queries multiple sources (Google, Bing, DuckDuckGo, etc.) simultaneously without tracking users or storing search logs. It is the privacy-respecting alternative to using a Google or Bing API directly.

## When to activate
Activate this skill when the user asks to:
- Search the web or internet for anything
- Look up current news, events, prices, or facts
- Find information that may be newer than your training data
- Research a topic online

## How to use

When this skill is relevant, call the `run_js` tool using `index.html` with a JSON string for `data` containing these fields:

- `query`: Required. The search query string. Extract the core search intent from the user's message. Keep it concise and specific (e.g. "Sydney weather today", "best budget phone 2026").
- `num_results`: Optional. Number of results to return. Default is 5. Maximum is 10.

### Example tool call
```json
{
  "query": "latest developments in fusion energy 2026",
  "num_results": 5
}
```

## Handling results

The tool returns a JSON object with either:

**Success:**
```json
{
  "result": {
    "query": "the search query used",
    "results": [
      {
        "title": "Result title",
        "url": "https://example.com/page",
        "snippet": "A short description of the result..."
      }
    ],
    "source": "SearXNG (privacy-preserving meta-search)"
  }
}
```

**Error:**
```json
{
  "error": "Description of what went wrong"
}
```

## After receiving results

1. Summarise the most relevant results in 2-4 sentences addressing the user's question directly.
2. List the top results with their titles and URLs so the user can explore further.
3. Note if results seem outdated or if the query should be refined.
4. Keep your response concise — the on-device context window is limited.
5. Always end with a complete sentence.

## Important notes
- Results come from multiple search engines simultaneously via SearXNG's public instance
- No API key is required — this is fully free and privacy-preserving
- If the public SearXNG instance is rate-limited or unavailable, inform the user and suggest trying again shortly
- Do not fabricate results — only report what the tool returns
