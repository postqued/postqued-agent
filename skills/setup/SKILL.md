---
name: setup
description: Set up, authenticate, verify, or troubleshoot the Postqued Claude plugin and its API key. Use when the user asks to connect Postqued, configure credentials, fix authentication, check access, or diagnose why Postqued tools are unavailable.
---

# Set up Postqued

Postqued is connected through its first-party remote MCP server. Never ask the user to paste an API key into the conversation, and never print, log, or expose credentials.

## Configure access

1. Ask the user to sign in at `https://postqued.com`.
2. Direct them to **Settings → API** and have them create an organization-bound API key.
3. Have them enable the Postqued plugin in Claude and enter the key in the secure configuration prompt. The plugin marks this value as sensitive so supported Claude clients store it in their credential store.
4. Call `list_workspaces` to verify the connection.

Postqued API access requires an eligible paid plan. If authentication succeeds but API access is denied, ask the user to check the organization subscription and confirm that the key belongs to the intended organization.

## Troubleshoot

- For an authentication error, have the user replace or rotate the key in the plugin configuration. Do not request the key itself.
- If no workspace is returned, verify membership in the intended Postqued organization.
- If publishing tools are unavailable, confirm that at least one supported social account is connected in Postqued.
- If a tool call fails, report the actionable error without exposing request headers or credentials.
