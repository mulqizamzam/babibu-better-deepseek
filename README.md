# Babibu Better DeepSeek

A reconciled port of [EdgeTypE/dsh-better-deepseek](https://github.com/EdgeTypE/dsh-better-deepseek), maintained as a DeepSeek Harness (DSH) plugin.

**Target port version:** `0.2.1-rc.2`

This repository preserves the Better DeepSeek browser-extension bridge: session creation, prompt handoff, cancellation, session-result polling, and Server-Sent Events (SSE) for assistant and tool activity.

## Install

With DeepSeek Harness installed:

```bash
dsh plugin --profile web add github:mulqizamzam/babibu-better-deepseek
```

Or:

```bash
npx @deepseek-ai/dsh --profile web add github:mulqizamzam/babibu-better-deepseek
```

## Bridge endpoints

All routes are registered under `/api/better-deepseek`:

| Endpoint | Method | Purpose |
|---|---|---|
| `/ping` | GET | Handshake and capability report |
| `/events` | GET | SSE stream for session and tool events |
| `/session.create` | POST | Create a Harness agent session with a working directory |
| `/session.prompt` | POST | Submit a prompt to an existing session |
| `/session.result` | GET | Poll session status and final assistant text |
| `/session.cancel` | POST | Cancel an existing session |

## Configuration and security

The Cordis patch enables `enableCors: true` by default to support a local browser-extension client. This sets wildcard `Access-Control-Allow-Origin`; it is not authentication. Run Harness only in a trusted environment, do not expose its web server to untrusted networks, and disable CORS when cross-origin access is not needed.

## Development

The plugin is written in TypeScript and uses DeepSeek Harness workspace packages. The upstream workspace currently declares several dependencies as `workspace:^`; this port retains the Harness-native package contract. Build and test it within a compatible DSH workspace/release environment.

## Upstream and attribution

- Original bridge: [EdgeTypE/dsh-better-deepseek](https://github.com/EdgeTypE/dsh-better-deepseek)
- Companion extension: [EdgeTypE/better-deepseek](https://github.com/EdgeTypE/better-deepseek)
- This is an independent community port and is not affiliated with or endorsed by DeepSeek.

See [LICENSE](LICENSE) for licensing terms.
