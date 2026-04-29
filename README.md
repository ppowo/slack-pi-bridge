# Slack Pi Bridge

A small personal Slack DM bridge that uses [pi](https://github.com/mariozechner/pi) to generate concise replies to one selected Slack user. It polls a direct message channel, keeps a short local conversation history, and can run in dry-run mode so replies are logged before anything is sent.

## Features

- Replies only to the configured Slack member ID
- Uses pi with a Synthetic-hosted model for message generation
- Keeps local state and logs in OS-appropriate user directories
- Includes prompt-injection guardrails and reply sanitization
- Loads an optional gitignored identity context file so replies can better sound like you
- Supports `DRY_RUN=true` for safe testing

## Setup

```bash
npm install
cp .env.example .env
```

Fill in `.env`:

```env
SLACK_USER_TOKEN=xoxp-your-user-token
TARGET_USER_ID=U123456789
SYNTHETIC_API_KEY=your-key
IDENTITY_CONTEXT_FILE=.identity-context.txt
DRY_RUN=true
```

Your Slack token needs permission to open/read DMs and send messages.

Optionally create `.identity-context.txt` next to `.env` with private details the model may use when replying as you, for example your name, timezone, communication style, preferences, or other personal context. This file is gitignored by default.

Privacy note: the identity context is included in prompts sent to the configured model provider. Do not put secrets, credentials, or anything you do not want sent to that provider in this file.

## Run

```bash
npm start
```

Dry-run mode is enabled by default; generated replies are logged but not sent unless you set `DRY_RUN=false`.

## Build / check

```bash
npm run check
npm run build
```

## License

MIT
