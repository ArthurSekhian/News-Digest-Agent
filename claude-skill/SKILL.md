---
name: news-digest-agent-builder
description: Helps build, adapt, and debug scheduled Telegram/Slack digest bots for any topic using source-specific extractors.
---

# News Digest Agent Builder

Use this skill to help users build digest agents for any topic.

The goal is to turn selected sources into a scheduled Telegram or Slack digest.

## Core idea

Do not rely only on AI browsing for production digests.

Use source-specific extractors first.

Then use a sender script to:

- combine items
- deduplicate by URL
- format the digest
- send or print the result

## Architecture

```text
scheduler
  ↓
sender script
  ↓
extractor scripts
  ↓
structured items
  ↓
filter + deduplicate
  ↓
digest formatter
  ↓
Telegram / Slack delivery
```

## Extractor format

Each extractor should return items with:

- title
- url
- date
- source
- category
- score
- include
- reason

Extractor command format:

```bash
python3 extractors/examples/custom_topic_extract.py START_DATE END_DATE --included-only
```

## User workflow

Guide the user through small steps:

1. Choose a digest topic.
2. List sources to monitor.
3. Create one extractor per source.
4. Test each extractor.
5. Add extractors to the sender.
6. Test the sender locally.
7. Configure Telegram or Slack delivery.
8. Schedule the sender.

## Digest format

```text
Weekly {{Topic}} Digest

Period: YYYY-MM-DD — YYYY-MM-DD

1. {{Title}}
Date: {{Date}}
Category: {{Category}}
Score: {{Score}}/10

Why it matters:
2–4 concise sentences explaining what happened and why it matters.

URL:
{{URL}}

Bottom line:
• {{insight}}
```

## Style

Give short step-by-step instructions.

Use clear file paths.

Do not overwhelm the user.
