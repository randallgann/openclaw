# OpenClaw Agent Setup Research: client-onboarding Agent

**Researched:** 2026-04-09
**Confidence:** HIGH (all findings verified from source code and official docs)

---

## 1. Agent Creation Process

### CLI Command

```bash
openclaw agents add client-onboarding \
  --workspace ~/.openclaw/workspace-client-onboarding \
  --non-interactive
```

This creates:

- Agent entry in `~/.openclaw/openclaw.json` under `agents.list[]`
- Agent state directory at `~/.openclaw/agents/client-onboarding/agent/`
- Session store at `~/.openclaw/agents/client-onboarding/sessions/`
- The workspace directory itself (you populate the files)

### Manual Config Alternative

Add directly to `~/.openclaw/openclaw.json` in the `agents.list` array:

```json
{
  "id": "client-onboarding",
  "name": "Scout",
  "workspace": "/Users/rgann/.openclaw/workspace-client-onboarding",
  "agentDir": "/Users/rgann/.openclaw/agents/client-onboarding/agent",
  "identity": {
    "name": "Scout",
    "emoji": "🔍"
  }
}
```

### Set Identity After Creation

```bash
openclaw agents set-identity --agent client-onboarding --from-identity
# or explicitly:
openclaw agents set-identity --agent client-onboarding \
  --name "Scout" --emoji "🔍"
```

---

## 2. Workspace Files and Their Roles

The workspace is located at `~/.openclaw/workspace-client-onboarding/`. These files are loaded into the system prompt in a fixed order defined in `src/agents/system-prompt.ts`:

| File           | Load Order | Purpose                                                                                          |
| -------------- | ---------- | ------------------------------------------------------------------------------------------------ |
| `AGENTS.md`    | 10         | Operating instructions, session startup checklist, memory protocol                               |
| `SOUL.md`      | 20         | Persona, tone, boundaries. If present, the system prompt includes: "embody its persona and tone" |
| `IDENTITY.md`  | 30         | Name, creature type, vibe, emoji, avatar                                                         |
| `USER.md`      | 40         | Owner context (Randall's info, company context)                                                  |
| `TOOLS.md`     | 50         | Environment notes, available resources, external references                                      |
| `BOOTSTRAP.md` | 60         | First-run ritual for new conversations. Delete after initial setup                               |
| `MEMORY.md`    | 70         | Curated long-term memory (only loaded in main/private sessions)                                  |
| `HEARTBEAT.md` | dynamic    | Periodic heartbeat checklist (loaded below cache boundary)                                       |

**Key insight from source code:** `SOUL.md` gets special treatment. When detected, the system prompt adds: "If SOUL.md is present, embody its persona and tone. Avoid stiff, generic replies; follow its guidance unless higher-priority instructions override it."

### Existing Workspace Patterns (from Atlas and Beacon agents)

**IDENTITY.md pattern:**

```markdown
# IDENTITY.md - Who Am I?

- **Name:** Scout
- **Creature:** Client discovery agent -- a website needs detective
- **Vibe:** Curious, thorough, consultative. Asks smart questions and captures everything.
- **Emoji:** 🔍
- **Avatar:** _(none yet)_

---

Scout: uncovering what clients really need, one conversation at a time.
```

**SOUL.md pattern:** Define core truths, boundaries, vibe, and continuity rules. See Atlas's SOUL.md for a strong example. Keep it sharp and behavioral, not corporate.

**AGENTS.md pattern:** This is the operational brain. It should include:

1. Session startup sequence (which files to read on wake)
2. Conversation protocol (discovery questions, flow)
3. Memory write rules (when to save, where to save)
4. Output format requirements (what the onboarding brief should contain)
5. Red lines (what not to do)

**USER.md pattern:** Owner context -- Randall's info, GannSystems.Pro context, target market.

**BOOTSTRAP.md pattern:** First-contact interaction guide. Unlike AGENTS.md, this is specifically for the first message in a new conversation with a prospect.

**TOOLS.md pattern:** Available tools, communication channels, key references.

### Additional Workspace Files

- `memory/` directory -- daily logs as `memory/YYYY-MM-DD.md`
- `skills/` directory -- workspace-specific skills (highest precedence)
- `hooks/` directory -- per-agent hooks (disabled by default until enabled)

---

## 3. HTTP/API Routing (How `/v1/responses` Selects an Agent)

**Source:** `src/gateway/http-utils.ts` lines 270-282

The gateway resolves the agent for an HTTP request using this priority:

### Priority 1: `x-openclaw-agent-id` Header (or `x-openclaw-agent`)

```
x-openclaw-agent-id: client-onboarding
```

This is the most direct way. The header is checked first.

### Priority 2: Model Field in Request Body

The `model` field in the POST body can encode the agent ID:

```json
{
  "model": "openclaw/client-onboarding",
  "input": "Hello",
  "stream": true
}
```

Supported formats (from `src/gateway/http-utils.ts` line 219):

- `openclaw/client-onboarding` (slash separator)
- `openclaw:client-onboarding` (colon separator)
- `agent:client-onboarding` (agent prefix)

The regex pattern: `/^openclaw[:/](?<agentId>[a-z0-9][a-z0-9_-]{0,63})$/i`

### Priority 3: Default Agent Fallback

If neither header nor model encodes an agent, falls back to the default agent (first agent with `default: true`, or the first in the list, or `main`).

### Session Continuity

The `/v1/responses` endpoint maintains session continuity via:

- `x-openclaw-session-key` header for explicit session pinning
- `previous_response_id` field in the request body (maps to stored session keys in memory, TTL 30 min)
- `user` field in the request body (creates user-scoped sessions: `agent:<agentId>:responses-user:<userId>`)

### Practical Setup for Web App

Your web app should send:

```javascript
const response = await fetch("https://api.rgann-openclaw.work/v1/responses", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer <gateway-token>",
    "x-openclaw-agent-id": "client-onboarding",
    // Optional: pin to a specific session
    "x-openclaw-session-key": `agent:client-onboarding:onboard-${visitorId}`,
  },
  body: JSON.stringify({
    model: "openclaw", // or 'openclaw/client-onboarding'
    input: userMessage,
    stream: true,
  }),
});
```

**Either the header OR the model field works.** Using both is redundant but harmless (header takes precedence).

---

## 4. Channel Binding for Web/HTTP

### Web is NOT a Traditional Channel

The web/HTTP interface (`/v1/responses`, `/v1/chat/completions`) is **not** a channel in the binding system. It is a direct API endpoint. Unlike WhatsApp/Discord/Telegram, there is no `web` channel type in the binding config.

**This means:** You do NOT need a binding entry in `openclaw.json` for HTTP traffic. Agent selection happens via the header or model field as described above, not via channel routing.

### If You Wanted Channel-Based Routing

For messaging channels (WhatsApp, Discord, etc.), you would add bindings:

```json
{
  "bindings": [
    {
      "agentId": "client-onboarding",
      "match": { "channel": "whatsapp", "peer": { "kind": "direct", "id": "+1555XXXXXXX" } }
    }
  ]
}
```

But for the web app use case, **skip bindings entirely** and use the `x-openclaw-agent-id` header.

---

## 5. Session Completion Hooks

### Built-in Hook: `session-memory`

The `session-memory` hook fires on `command:new` and `command:reset`. It extracts the last 15 user/assistant messages, generates a slug via LLM, and saves to `<workspace>/memory/YYYY-MM-DD-slug.md`.

```bash
openclaw hooks enable session-memory
```

### Custom Hooks for Session Completion

There is **no built-in "session complete" event**. However, you can approximate it:

**Option A: `command:new` / `command:reset` hooks** -- Fire when the user starts a new session or resets. The hook receives the previous session context and can generate output.

**Option B: `message:sent` hook** -- Fires after every outbound message. You could use this to detect a "conversation complete" signal (e.g., the agent says a specific phrase).

**Option C: Agent-driven approach (recommended)** -- Instruct the agent in AGENTS.md to write a summary brief to a specific file when the discovery conversation is complete. The agent has `write` and `edit` tools and can create files in the workspace. Example instruction:

```markdown
## Completion Protocol

When you have gathered enough information to write a client brief:

1. Write the brief to `briefs/YYYY-MM-DD-<company-slug>.md`
2. Include: company name, industry, size, pain points, current tools, recommended solutions, estimated budget range
3. Tell the client: "I've captured everything. Randall will review and follow up with a detailed proposal."
4. Update `memory/YYYY-MM-DD.md` with a summary of the conversation
```

**Option D: Custom workspace hook** -- Create a hook at `~/.openclaw/workspace-client-onboarding/hooks/onboarding-complete/`:

```
onboarding-complete/
  HOOK.md          # events: ["command:new"]
  handler.ts       # Generates brief from session history
```

### Hook Event Context

Command hooks receive:

- `event.context.sessionEntry` -- current session
- `event.context.previousSessionEntry` -- previous session (useful for generating summary)
- `event.context.workspaceDir` -- workspace path
- `event.context.cfg` -- full config

Message hooks receive:

- `event.context.from` / `event.context.to`
- `event.context.content`
- `event.context.channelId`
- `event.context.metadata` (includes `senderId`, `senderName`)

---

## 6. System Prompt Assembly and Precedence

**Source:** `src/agents/system-prompt.ts`

The system prompt is assembled in this order (top = highest priority in the prompt):

1. **Core identity line** -- Basic "You are OpenClaw" preamble
2. **AGENTS.md** (order 10) -- Operating instructions
3. **SOUL.md** (order 20) -- Persona and tone (with special "embody" instruction)
4. **IDENTITY.md** (order 30) -- Name, vibe, emoji
5. **USER.md** (order 40) -- Owner context
6. **TOOLS.md** (order 50) -- Environment notes
7. **BOOTSTRAP.md** (order 60) -- First-run ritual
8. **MEMORY.md** (order 70) -- Long-term memory (main session only)
9. **Skills section** -- Available skills (if configured)
10. **Memory search section** -- Memory tool instructions
11. **Heartbeat section** -- Heartbeat prompt (if configured, not for subagents)
12. **Dynamic files** -- `HEARTBEAT.md` placed below cache boundary
13. **Provider contributions** -- Model-specific prompt sections from plugins

### Prompt Modes

- `"full"` -- All sections (default for main agent turns)
- `"minimal"` -- Reduced sections for subagents (Tooling, Workspace, Runtime only)
- `"none"` -- Just basic identity line

### Key Behavior

- All workspace `.md` files are injected as `## <filename>` sections in the system prompt
- SOUL.md is the personality driver -- the system prompt explicitly tells the model to "embody its persona and tone"
- AGENTS.md is the operational brain -- rules, protocols, memory instructions
- Files are sorted deterministically by the order map, ensuring prompt cache stability

---

## 7. Complete Setup Walkthrough

### Step 1: Create the Agent

```bash
openclaw agents add client-onboarding \
  --workspace ~/.openclaw/workspace-client-onboarding \
  --non-interactive
```

### Step 2: Create Workspace Files

```bash
mkdir -p ~/.openclaw/workspace-client-onboarding/memory
mkdir -p ~/.openclaw/workspace-client-onboarding/briefs
```

Create these files in `~/.openclaw/workspace-client-onboarding/`:

- `IDENTITY.md` -- Agent name, vibe
- `SOUL.md` -- Personality, tone, boundaries
- `AGENTS.md` -- Discovery conversation protocol, memory rules, brief generation
- `USER.md` -- Randall/GannSystems context
- `TOOLS.md` -- Available resources
- `BOOTSTRAP.md` -- First-contact interaction guide

### Step 3: Set Identity

```bash
openclaw agents set-identity --agent client-onboarding --from-identity
```

### Step 4: Enable Hooks (Optional)

```bash
openclaw hooks enable session-memory
```

### Step 5: Update Config (if needed)

The `agents add` command handles config, but verify in `~/.openclaw/openclaw.json`:

```json
{
  "agents": {
    "list": [
      // ... existing agents ...
      {
        "id": "client-onboarding",
        "name": "Scout",
        "workspace": "/Users/rgann/.openclaw/workspace-client-onboarding",
        "agentDir": "/Users/rgann/.openclaw/agents/client-onboarding/agent",
        "identity": {
          "name": "Scout",
          "emoji": "🔍"
        }
      }
    ]
  }
}
```

### Step 6: Configure Model (Optional Per-Agent Override)

Add per-agent model if you want this agent to use a different model:

```json
{
  "id": "client-onboarding",
  "model": "anthropic/claude-sonnet-4-5"
  // ... rest of config
}
```

Without this, it inherits from `agents.defaults.model`.

### Step 7: Restart Gateway

```bash
openclaw gateway restart
openclaw agents list --bindings
```

### Step 8: Test via API

```bash
curl -X POST http://localhost:18789/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <gateway-token>" \
  -H "x-openclaw-agent-id: client-onboarding" \
  -d '{"model":"openclaw","input":"Hi, I run a small plumbing company","stream":false}'
```

---

## 8. Web App Integration Notes

### Agent Selection

Use **one** of these approaches (not both):

| Method      | How                                      | When to Use                                     |
| ----------- | ---------------------------------------- | ----------------------------------------------- |
| Header      | `x-openclaw-agent-id: client-onboarding` | Preferred. Explicit, works with any model value |
| Model field | `"model": "openclaw/client-onboarding"`  | Alternative. Encodes agent in the model string  |

### Session Management

- **Anonymous visitors**: Let the gateway auto-generate session keys (each response gets a fresh session unless `previous_response_id` is used)
- **Tracked visitors**: Send `"user": "visitor-<uuid>"` in the request body to create user-scoped sessions
- **Explicit sessions**: Use `x-openclaw-session-key` header for full control

### Session Continuity with `previous_response_id`

The `/v1/responses` endpoint supports conversation threading via `previous_response_id`. Each response includes an `id` field. Pass it back as `previous_response_id` in the next request to continue the same session. Session mappings live in memory with a 30-minute TTL.

### Model Override

To override the agent's default model per-request:

```
x-openclaw-model: anthropic/claude-sonnet-4-5
```

---

## 9. Pitfalls and Gotchas

1. **Auth profiles are per-agent.** The new agent needs its own API keys at `~/.openclaw/agents/client-onboarding/agent/auth-profiles.json`. Copy from the main agent if sharing keys: `cp ~/.openclaw/agents/main/agent/auth-profiles.json ~/.openclaw/agents/client-onboarding/agent/auth-profiles.json`

2. **Never reuse `agentDir` across agents.** This causes auth/session collisions.

3. **Config is strict JSON.** No comments allowed in `openclaw.json`. Unknown keys cause startup failure.

4. **BOOTSTRAP.md is one-time.** Delete it after the first-run ritual is complete, or it will be injected every session.

5. **MEMORY.md only loads in main/private sessions.** Not in group or shared contexts.

6. **Session TTL for responses endpoint.** The `previous_response_id` mapping expires after 30 minutes of inactivity. For longer conversations, use explicit `x-openclaw-session-key`.

7. **Web/HTTP is not a channel.** Do not try to add `"web"` bindings in the config. Use the header or model field instead.

8. **Bootstrap file size limits.** Individual files are truncated at 20,000 chars (configurable via `agents.defaults.bootstrapMaxChars`). Total across all files: 150,000 chars (`agents.defaults.bootstrapTotalMaxChars`).

9. **Gateway restart required.** After config changes, restart the gateway: `openclaw gateway restart`.

10. **Hook workspace scope.** Workspace hooks in `<workspace>/hooks/` are disabled by default. You must explicitly enable them with `openclaw hooks enable <name>`.
