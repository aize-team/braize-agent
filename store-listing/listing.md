# Store listing copy: Braize | Agent unlimited memory

One copy deck for every store. Character counts are for the strictest store limits we
know of; check each store's form when submitting (see the publishing plan).

## Title

**Braize | Agent unlimited memory**  (31 chars)

Short fallback where `|` or length is rejected: **Braize Memory**

> Honesty note (owner decision): plans have indexed-page and monthly-query limits
> (`plans.json`: free = 100 pages / 200 queries). "Unlimited" in the title must not be
> read as unlimited storage. The copy below says what is actually true: memory that
> doesn't fade and grows with your plan, not a limitless store. Some reviewers
> (OpenAI, Anthropic directory) reject unqualified "unlimited" claims. Keep **Braize
> Memory** ready as the fallback title.

## Tagline (≤ 80 chars)

Permission-aware company memory your agents can cite. Always synced, never stale.  (79)

## Short description (≤ 160 chars)

Give any AI agent your team's knowledge: synced from your tools, permission-aware, freshness-checked, and returned as cited passages in about three seconds.  (155; the 3 s is the production retrieve median, 2.8 s)

## Long description

Agents forget. Your company's knowledge keeps changing. Braize closes the gap.

Braize connects to the places your team already keeps its knowledge. It keeps every
document in sync, flags what has gone stale, and gives your agents one permission-aware
memory to search. Ask from Claude, ChatGPT, Gemini, Cursor or any MCP-capable agent and
get ranked passages back, each with its source, so the agent can quote it instead of
guessing.

**What your agent gets**

- **Cited passages, fast.** `search_knowledge` returns ranked passages with titles and
  source references. In our production benchmark (v1.6.18, 116 questions whose sources
  were indexed) it found the right passage 98.3% of the time, with a median of 2.8 seconds.
- **Permission-aware by design.** Each person reads only what they can already see in the
  source. Permissions are checked inside the search itself, not filtered afterwards.
  Anonymous connections see public content only.
- **Freshness you can check.** Agents can ask how current the knowledge is and which
  documents are going stale, before they quote a price or a policy.
- **Memory that persists.** Agents can write and recall their own notes across sessions
  (MCP and REST API; with sign-in, each person's notes stay private).
- **One knowledge layer for every agent.** The same knowledge serves every MCP-capable
  agent and your own code through the REST API.

**How it works**

1. Connect your sources in the Braize dashboard. See the live list of supported
   connectors at br.aize.dev.
2. Add Braize to your agent: sign in over MCP, or use a workspace API key.
3. Ask. Your agent searches, reads the cited passages and answers.

**Plans:** a free plan to start, with paid plans for more indexed pages, queries and
connectors. Limits per plan are listed at br.aize.dev/pricing.

**Privacy:** br.aize.dev/privacy · **Terms:** br.aize.dev/terms · **Security:** br.aize.dev/security

## Keywords / categories

memory, knowledge base, company knowledge, RAG, search, citations, enterprise search,
productivity, MCP. Category: Productivity (fallback: Developer tools / Business).

## Example prompts (for store "try it" fields)

1. "What does our refund policy say about annual plans? Cite the source."
2. "Which of our documents are stale right now?"
3. "What sources are connected to our knowledge base?"
4. "Find everything we've written about onboarding a new customer."

## Assets needed (owner to supply or approve)

- Icon: square PNG, 512–2048 px, under 2 MB, no SVG/WebP (Claude plugin validator); ChatGPT
  accepts ≥ 48 px PNG/JPEG/WebP/SVG ≤ 5 MiB. Candidate already in the plugin:
  `plugins/braize/.claude-plugin/icon.png` (copy of `services/dashboard/app/icon.png`, 512×512).
  **The Claude directory locks the icon at the first portal save**, so the owner approves it first.
- 3–5 screenshots (1280×800 or 1920×1080): an agent answering with Braize citations in
  Claude, ChatGPT, Cursor; the dashboard source list; the freshness report.
- Demo video, 30–60 s (optional; some directories ask for it).
- Support email and URL, privacy policy URL, terms URL (all exist under br.aize.dev).
