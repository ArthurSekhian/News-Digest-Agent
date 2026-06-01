# Architecture

News Digest Agent uses a local-first pipeline.

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

## Components

### Extractors

Extractors collect updates from specific sources.

Each extractor returns structured JSON items.

### Sender

The sender runs extractors, combines their output, removes duplicates, formats the digest, and sends or prints it.

### Scheduler

The scheduler runs the sender on a fixed schedule.

Examples:

- cron
- OpenClaw
- GitHub Actions
- another automation tool

## Core principle

Do not rely only on AI browsing for production digests.

Use source-specific extractors first.
