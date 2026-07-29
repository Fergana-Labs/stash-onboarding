# Capability gates

What the product actually exposes today, and the rule that follows from it.
Verified against `../moltchat` on 2026-07-28.

| Capability | Current production surface | Onboarding rule |
|---|---|---|
| Install | `bash -c "$(curl -fsSL https://joinstash.ai/install)"` | Interactive; let the user pick agents and session import. |
| Authenticate | `stash signin` | Let the user complete browser or API-key auth; never collect credentials. |
| Install hooks | Interactive `stash signin` detects agents and installs hooks | Respect printed restart and trust steps, especially Codex hook approval. |
| Verify uploads | `stash status --json` | Require a real successful upload before calling capture healthy. |
| Browse sources | `stash ls / --json`, `stash vfs` | Inventory what is actually visible, not what should be. |
| Connect sources | `stash sources add`, `stash sources sync` | Use only supported, user-approved connectors. Never silently substitute one. |
| Read integrations | MCP tools available to the session | The curator reads these live. There is no unified change feed — coverage comes from the wiki's own source map and run log. |
| Curate | `stash-curate-memory` skill, writing to a local memory root | Curation is a folder operation. Do not treat the memory root as synced until it is uploaded. |
| Trigger cloud curator | `stash memory --recompute --json` | Recomputes Stash-side memory. Do not run it against a wiki the local curator owns — one writer per wiki. |
| Fetch local prompt | `GET /api/v1/me/local-curator-prompt` | Desktop/runtime capability, not a CLI command. |
| Publish the wiki | `stash upload <path> --json` | Ask before uploading; record the returned path in the brief. |
| Inspect memory | `stash memory --json`, `stash ls /memory --json` | Verify the output and link the user to the resulting folder. |
| OpenClaw/Hermes capture | Existing Stash plugins and hooks | Session capture exists; dynamic route injection does not. |
| Always-loaded guidance | Not exposed by current hooks | Requires a session-start hook that injects the agent guidance. Until then, the retrieval skill must be invoked explicitly. |

Never reinterpret an unavailable capability as optional. Report it as a product
dependency.
