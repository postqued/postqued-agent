# Postqued for Claude

The official Postqued plugin for Claude. Plan, upload, schedule, publish, review, and analyze social media without leaving your conversation.

Postqued connects Claude to the first-party Postqued MCP server and provides guidance for safe publishing, approval workflows, engagement, and account management.

## What you can do

- Create, upload, schedule, reschedule, and publish social content
- Work across connected social accounts and Postqued workspaces
- Inspect publishing status and account analytics
- Manage comments and engagement
- Run internal approvals and client review workflows
- Invite and manage collaborators and reviewers

## Requirements

- A current version of Claude Code or another Claude client that supports plugins
- A Postqued account with API access on an eligible paid plan
- A Postqued organization API key
- At least one connected social account for publishing

Create an organization-bound key from **Postqued → Settings → API**. Claude requests the key when you enable the plugin. The manifest marks it as sensitive so supported Claude clients store it in their secure credential store rather than in this repository.

Never paste your API key into a conversation or commit it to source control.

## Install

### Test from this repository

```sh
git clone https://github.com/postqued/postqued-agent.git
claude --plugin-dir ./postqued-agent
```

### Community directory

Once approved in Anthropic's community directory:

```sh
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install postqued@claude-community
```

Enable the plugin, enter your Postqued API key in Claude's secure prompt, and ask Claude to list your Postqued workspaces to verify the connection.

## Example prompts

- “Show my connected Postqued accounts.”
- “Draft an Instagram post using this image and validate it before publishing.”
- “Schedule this campaign for tomorrow at 10:00 in Europe/London.”
- “Show the status of my recent publishing requests.”
- “Summarize account analytics for the last 30 days.”
- “List posts awaiting my approval.”

Claude validates publishing requests with a dry run and asks for confirmation before real publication or other sensitive changes.

## Permissions and data

This plugin connects only to `https://mcp.postqued.com/mcp`. It does not install hooks or execute local scripts. Depending on your request, its tools can read and modify data in your Postqued organization, including social content, publishing schedules, comments, approvals, collaborators, and connected accounts.

Review the [Postqued privacy policy](https://postqued.com/privacy) and [terms of service](https://postqued.com/terms).

## Development

Validate the plugin with Anthropic's current Claude Code CLI:

```sh
claude plugin validate . --strict
```

The plugin uses Anthropic's standard directory layout:

```text
.claude-plugin/plugin.json
.mcp.json
skills/setup/SKILL.md
skills/social-media/SKILL.md
```

## Security

Do not open a public issue containing an API key or other sensitive information. See [SECURITY.md](SECURITY.md) for reporting instructions.

## License

[MIT](LICENSE)
