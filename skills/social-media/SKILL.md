---
name: social-media
description: Manage social media with Postqued, including connected accounts, media uploads, drafts, scheduling, publishing, analytics, comments, approval workflows, collaborators, and client reviews. Use whenever the user asks Claude to create, inspect, schedule, publish, reschedule, cancel, analyze, approve, or collaborate on social content through Postqued.
---

# Use Postqued

Use only the Postqued MCP tools supplied by this plugin. Do not call undocumented Postqued HTTP endpoints or invent parameters. Let the live tool schemas determine supported fields and platform options.

## Establish context

1. Call `list_workspaces` before workspace-scoped work unless the current conversation already identifies one unambiguously.
2. If multiple workspaces could match, show their names and ask the user to choose. Never guess a workspace ID.
3. Call `list_accounts` before platform-specific work. Use `get_workspace_capabilities` when plan or feature availability matters.

## Prepare content

- Use `start_content_upload` and `complete_content_upload` for media. Do not claim an upload completed until the completion tool succeeds.
- Use the relevant platform helper before composing platform-specific settings. Examples include Reddit restrictions, Pinterest boards, LinkedIn companies, Instagram audio, and creator information.
- Keep captions, media, destinations, scheduling, and platform-specific settings explicit in the summary shown to the user.

## Publish safely

1. Call `publish_content` with `dryRun: true` to validate a proposed publish or schedule operation.
2. Present the validated destinations, timing, content summary, and any warnings.
3. Obtain explicit confirmation immediately before a real publish, schedule, reschedule, or cancellation unless the user already gave clear approval for those exact details in the current turn.
4. For the real `publish_content` call, set `dryRun: false` and provide a fresh UUID as `idempotencyKey`.
5. Use `get_publish_status` or `list_publish_requests` for durable status. Do not treat queue acceptance as successful publication.

Never silently retry a real publish with a new idempotency key. First inspect its persisted status so duplicate posts are not created.

## Approvals and collaboration

- Treat approval and client-review versions as concurrent state. Refresh the post or review before accepting suggestions, approving, requesting changes, scheduling, or publishing.
- Preserve reviewer feedback and identify the exact revision being acted on.
- Confirm the target person and role before invitations, permission changes, removals, or revocations.

## Engagement and destructive changes

- Show the exact account, post or comment, and intended action before replying, hiding, liking, deleting, or changing access.
- Require explicit confirmation before deletions, disconnecting accounts, removing collaborators or reviewers, or publishing a reply/comment.
- Prefer reversible operations where the tools offer them.

## Responses

After each action, state what changed, where it changed, and its current status. Include human-readable names and timestamps; include opaque IDs only when useful for follow-up or support.
