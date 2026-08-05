# Awesome Engineering AI [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

> Tools you can actually install and use **with** your coding agent — skills, MCP servers, harnesses, CLIs.

Most "awesome AI" lists are directories of everything that mentions an LLM. This one is the opposite: it is the residue of a weekly radar that scans GitHub Trending, Hacker News, Reddit and X every day and throws away almost everything it finds.

Two gates decide whether a tool gets in.

**1. What does a developer do differently tomorrow, at their keyboard, because this exists?** No answer — no entry.

**2. At least 500 stars.** Not a ranking, a floor. A three-star repository published yesterday may well be better than anything here, but nobody has run it on a real codebase yet, and most of them are gone within a month. This list is a filter, not a discovery feed — go to GitHub Trending for day zero. For the handful of entries that are products rather than repositories, the equivalent bar is a public track record.

**Out of scope, on purpose:** frameworks for *building* agents (LangChain, AG2, AutoGen, CrewAI-the-framework), model releases and pricing, protocol politics, domain MCP servers (stock tickers, CRMs), listicles, "awesome" hubs that just link elsewhere, and consumer AI products. What is left is what you can `git clone`, `npx`, or drop into `.claude/skills/` today.

Curated by [Nikita Pastukhov](https://github.com/Lancetnik) — [FastStream](https://github.com/ag2ai/faststream) author, [AG2](https://github.com/ag2ai/ag2) co-maintainer. Most entries come from the weekly *agent tooling radar* published on my Telegram channel [@fastnewsdev](https://t.me/fastnewsdev) (RU).

## Legend

Everything on this list passed both gates. The marks say how much of it I have personally run:

| Mark | Meaning |
|---|---|
| 🥇 | **Daily driver.** In my everyday setup, would reinstall on a fresh machine. |
| ✅ | Tried it, recommend it. |
| 🧪 | Tried it, verdict still open — or works, with a caveat worth knowing. |
| ❌ | Tried it, did not stick for me. Listed because it is popular and your mileage may differ. |
| *(none)* | Passed the filter on the radar, not personally tested yet. |

An ❌ is a personal verdict, not a quality judgement — several of them have far more stars than anything I use.

## Contents

- [Awesome Engineering AI ](#awesome-engineering-ai-)
  - [Legend](#legend)
  - [Contents](#contents)
  - [Skill libraries](#skill-libraries)
  - [Building and tuning your own skills](#building-and-tuning-your-own-skills)
  - [Spec-driven development](#spec-driven-development)
  - [Context, retrieval and memory](#context-retrieval-and-memory)
  - [Review, guardrails and forensics](#review-guardrails-and-forensics)
  - [Security: pentest, reverse engineering and audit](#security-pentest-reverse-engineering-and-audit)
  - [Harnesses, GUIs and workspaces](#harnesses-guis-and-workspaces)
  - [Coding agent CLIs](#coding-agent-clis)
  - [Orchestration and agent fleets](#orchestration-and-agent-fleets)
  - [Web, research and monitoring](#web-research-and-monitoring)
  - [Beyond code: video, mobile, motion](#beyond-code-video-mobile-motion)
  - [Model gateways and routing](#model-gateways-and-routing)
  - [Integrations and credential brokering](#integrations-and-credential-brokering)
  - [Design and UI quality](#design-and-ui-quality)
  - [Output discipline](#output-discipline)
  - [Directories and reference](#directories-and-reference)
  - [How this list is maintained](#how-this-list-is-maintained)
  - [Contributing](#contributing)
  - [License](#license)

## Skill libraries

Whole setups you install at once, instead of collecting skills one by one. The pattern of 2026: a role, not a task. Two verticals grew big enough to get their own sections: [Design and UI quality](#design-and-ui-quality) and [Security](#security-pentest-reverse-engineering-and-audit).

- 🥇 **[mattpocock/skills](https://github.com/mattpocock/skills)** — "Skills for real engineers": Matt Pocock's working `.claude` directory, published as-is. Ships [grill-with-docs](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs), the single skill I would keep if I could keep only one — it interrogates you until the task is actually specified, writes the decision into an ADR, and maintains a project glossary in `CONTEXT.md`. After a few sessions you and the agent speak the same language. Its [prototype](https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype) skill is listed separately under [Design and UI quality](#design-and-ui-quality).
- **[gstack](https://github.com/garrytan/gstack)** — Garry Tan's opinionated Claude Code setup: 23 tools split across CEO / Designer / Eng Manager / Release Manager / Doc Engineer / QA roles.
- **[andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills)** — the minimal end of the pattern: a single `CLAUDE.md` distilled from Karpathy's observations about how LLMs actually write code. No install, no directory tree — one file that changes the agent's defaults.

## Building and tuning your own skills

- **[book-to-skill](https://github.com/virgiliojr94/book-to-skill)** — turns a PDF of a technical book, a docs folder or a set of sources into one installable skill for Claude Code / Copilot CLI / Amp. Your shelf reference becomes something the agent consults mid-task.
- **[cangjie-skill](https://github.com/kangarooking/cangjie-skill)** — same direction, wider input: books, long videos and podcasts distilled into executable skills.
- **[microsoft/SkillOpt](https://github.com/microsoft/SkillOpt)** — trains a skill like a model: epochs, batch size, learning rate, validation gates, no weights touched; output is a deployable `best_skill.md`. Research-flavoured — you need trajectories and a validation set, so it is less "install and go" than the rest of this section.
- **[HKUDS/OpenSpace](https://github.com/HKUDS/OpenSpace)** — a management layer for skills: organize them and attach them to agents, self-hosted.
- **[writing-great-skills](https://github.com/mattpocock/skills/blob/main/skills/productivity/writing-great-skills/SKILL.md)** — a skill for writing skills: the conventions that separate one the agent actually invokes from one it ignores. Start here before hand-rolling your first.
- **[agents-best-practices](https://github.com/DenisSergeevitch/agents-best-practices)** — provider-neutral guidance for Codex, Claude Code and harness design, shipped as a skill rather than a blog post, so the agent applies it while helping you build your own.

## Spec-driven development

Fix the spec, derive the plan, derive the tasks, and only then let the agent write code. Everything here is a variation on that loop; they differ in how much process they impose.

- 🥇 **[grill-with-docs](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs)** — the light end of SDD: questions until the task is unambiguous, an ADR, a running project glossary. No process change required.
- ✅ **[superpowers](https://github.com/obra/superpowers)** — brainstorm with probing questions → plan mode → TDD execution, through hard checkpoints. The workhorse, with one annoyance: by default it commits every plan and research note it generates into your repo, and a plan is an intermediate artifact — it belongs in the bin after the merge, not in git history. The sub-agent execution mode is also worth turning off when one focused agent would do.
- **[wayfinder](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder)** — for work too big to hold in one agent session: charts it as a map of *decision* tickets on your issue tracker — questions whose resolution is a decision, not slices of a build — and works them one at a time until the route is clear. Plans, deliberately does not execute; the urge to start building is the signal you have reached the edge of the map. Readers of my channel chat run it paired with grill-with-docs and report it holds up across sessions.
- **[github/spec-kit](https://github.com/github/spec-kit)** — GitHub's SDD toolkit: Specify → Plan → Tasks → Implement, on top of 30+ agents. The most popular of the bunch.
- **[Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)** — built for changes to a *living* project: specs are the source of truth about current state, every change goes through proposal → apply → archive.
- **[Q00/ouroboros](https://github.com/Q00/ouroboros)** — "stop prompting, start specifying": a replayable, specification-first workflow. Shares a name with [razzant/ouroboros](https://github.com/razzant/ouroboros), a self-modifying agent, and nothing else — if you arrived looking for the one with the benchmark claims, that is the other one.
- **[BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD)** — simulates a whole agile team, 12+ role agents (analyst, PM, architect, QA), each handing versioned artifacts to the next.
- **[Task Master](https://github.com/eyaltoledano/claude-task-master)** — turns a PRD into a dependency graph of tasks: the AI as project manager rather than implementer.
- **[Kiro](https://kiro.dev)** (AWS) — a VS Code fork where the spec is the central artifact: write requirements, the IDE generates design and tasks, agents execute.
- **[Tessl](https://tessl.io)** — enterprise take: spec as the primary artifact, code as regenerable output, plus a skill marketplace and evaluations.

## Context, retrieval and memory

The single biggest lever on agent quality and cost: stop it from reading half the repository to answer one question — and stop it from forgetting the answer next session.

- ✅ **[codegraph](https://github.com/colbymchenry/codegraph)** — builds an AST graph of the project via tree-sitter: symbols, calls, dependencies. Instead of blind `grep`, the agent asks precise questions — who calls this, what breaks if I change it, show me the signature — and gets a structural answer in milliseconds.
- 🧪 **[Graphify](https://github.com/Graphify-Labs/graphify)** — same idea, wider input: code, SQL schemas, infra, docs, articles, images and video into one queryable knowledge graph. Works as a skill across Claude Code, Codex, OpenCode, Cursor and Gemini CLI.
- 🧪 **[code-review-graph](https://github.com/tirth8205/code-review-graph)** — local-first persistent map of the repo, exposed over MCP and CLI, so the agent reads only what is relevant. Benchmarked context reductions on reviews and large repos.
- **[serena](https://github.com/oraios/serena)** — semantic retrieval *and* editing over MCP: the agent works on symbols through language servers instead of reading and rewriting whole files. The heaviest hitter in this section and the one to try first if you only try one.
- **[Understand Anything](https://github.com/Egonex-AI/Understand-Anything)** — the graph aimed at *you*, not only the agent: `/understand` runs a multi-agent pipeline over the project and produces an interactive dashboard you pan, search and click through, with plain-English summaries per node and a domain view mapping code to business processes. The onboarding case — 200k lines and no idea where to start. Installs as a plugin across Claude Code, Codex, Cursor, Copilot, Gemini CLI and opencode; the first run is expensive on a large repo, later runs are incremental.
- **[GitNexus](https://github.com/abhigyanpatwari/GitNexus)** — client-side code knowledge graph with no server to run: the same idea as codegraph, minus the setup.
- **[repomix](https://github.com/yamadashy/repomix)** — the blunt instrument of the section: packs an entire repository into one AI-friendly file. Useless for a large monorepo, unbeatable for handing a small project to a model in one shot.
- **[jcodemunch-mcp](https://github.com/jgravelle/jcodemunch-mcp)** — symbol-level retrieval from *remote* GitHub repositories over tree-sitter AST, rather than a local index.
- **[context-mode](https://github.com/mksglu/context-mode)** — sandboxes tool output, persists session memory, routes across platforms via MCP and hooks; claims up to 98% token reduction on tool results.
- **[headroom](https://github.com/headroomlabs-ai/headroom)** — the other half of the problem: everything above narrows *what* the agent reads, this one squeezes whatever came back. Tool output, logs, files and RAG chunks are compressed before the model ever sees them — 60–95% fewer tokens on JSON, around 20% on an ordinary coding agent, with the answers unchanged. Ships as a library, a proxy or an MCP server, so it slots in front of an agent you do not have to modify.
- **[agentmemory](https://github.com/rohitg00/agentmemory)** — persistent memory for coding agents, benchmarked rather than asserted. The one survivor of a memory wave that produced six tools in a single radar week: everything else that promised to fix "the agent forgets between sessions" is still below the star floor.
- 🧪 **[rtk](https://github.com/rtk-ai/rtk)** — proxies CLI commands and hands the agent a compressed digest instead of a wall of output. Stuck for me in a narrow niche: git, `ls`, `wc` — anything whose output is fat and whose useful part is three lines. Turn it off around test runs, where it only gets in the way.

## Review, guardrails and forensics

Everything that checks or constrains what the agent did — before, during and after. Security work proper is [its own section](#security-pentest-reverse-engineering-and-audit); this one is about your own diffs and your own machine.

- **[alibaba/open-code-review](https://github.com/alibaba/open-code-review)** — hybrid reviewer: deterministic pipelines plus an LLM agent, line-level comments, a fine-tuned built-in ruleset (NPE, thread safety, XSS, SQL injection). OpenAI- and Anthropic-compatible.
- **[react-doctor](https://github.com/millionco/react-doctor)** — catches the bad React your agent writes.
- **[tuicr](https://github.com/agavra/tuicr)** — the human half of the loop: a terminal code reviewer with vim bindings, line-level comments, per-file/hunk seen-tracking across sessions, and export to GitHub/GitLab. Reviews uncommitted changes — exactly the diff your agent just produced.
- **[dcg](https://github.com/Dicklesworthstone/destructive_command_guard)** — blocks destructive git and shell commands before the agent executes them; a guard layer over any CLI agent.
- **[Mindwalk](https://github.com/cosmtrek/mindwalk)** — replays an agent session on a 3D map of the codebase: where it walked, what it touched.

## Security: pentest, reverse engineering and audit

The other direction: not protecting your repo from the agent, but pointing the agent at a target. Two shapes have emerged — autonomous agents you aim at an application, and skill packs that hand your existing agent a security toolchain.

Everything here is for systems you own or are authorized to test.

- **[strix](https://github.com/usestrix/strix)** — autonomous open-source pentester: point it at your app, it finds and fixes vulnerabilities. A standalone agent rather than a plugin, which makes it the one to reach for when you have no security engineer at all.
- **[zhaoxuya520/reverse-skill](https://github.com/zhaoxuya520/reverse-skill)** — reverse engineering and authorized pentest skills, interesting less for the vertical than for the architecture: a *router* that picks the right skill per task, bootstraps the toolchain on the fly and writes back to its own knowledge base. The step after flat skill libraries.
- **[0x4m4/hexstrike-ai](https://github.com/0x4m4/hexstrike-ai)** — MCP server wrapping 150+ pentest tools; the same "hand the agent a toolchain" idea, without the router.
- **[vercel-labs/deepsec](https://github.com/vercel-labs/deepsec)** — a harness that runs coding agents across your codebase hunting vulnerabilities. Closest to ordinary review of the group: it reads your code rather than attacking a running system.
- **[trailofbits/skills](https://github.com/trailofbits/skills)** — Claude Code skills for security research, vulnerability detection and audit workflows, from a firm that audits for a living. The audit-methodology end of the section, not the exploit end.
- **[garak](https://github.com/NVIDIA/garak)** (NVIDIA) — the target here is the model, not the codebase: an LLM vulnerability scanner you point at your own agent or chatbot to probe prompt injection, jailbreaks and the rest before someone else does.

## Harnesses, GUIs and workspaces

Layers over the agent CLI: a UI, a workspace, or a bundle of capabilities.

- **[openwork](https://github.com/different-ai/openwork)** — self-hosted alternative to Claude Cowork built on opencode: a local environment for agent coding sessions, no cloud product attached.
- **[t3code](https://github.com/pingdotgg/t3code)** — minimal web GUI over Codex / Claude / Cursor / OpenCode from a single interface; `npx t3@latest` or a desktop app.
- **[cc-haha](https://github.com/NanmiCoder/cc-haha)** — local-first desktop workspace over Claude Code: multi-agent, git worktrees, diffs, a skill marketplace, multi-model, computer use, plus messenger front-ends.
- **[ECC](https://github.com/affaan-m/ECC)** — an installable capability layer over Claude Code / Codex / Opencode / Cursor: skills, instincts, memory, security and a research-first process.
- **[jcode](https://github.com/1jehuang/jcode)** — a deliberately minimal harness, tuned for low RAM against the GUI-heavy alternatives.
- **[claude-code-templates](https://github.com/davila7/claude-code-templates)** — CLI for configuring and monitoring Claude Code: agent, command and hook templates.

## Coding agent CLIs

The harness and the model are separate purchases. Everything here runs against a provider you choose — a local model, a cheaper API, your existing subscription — which is the whole reason to look past the vendor's own client.

- **[opencode](https://github.com/anomalyco/opencode)** — the reference open-source coding agent, and the substrate half this list builds on: provider-agnostic from the start, so the same terminal workflow runs on Anthropic, OpenAI, a local model, or whatever is cheapest this month.
- **[codex](https://github.com/openai/codex)** — OpenAI's lightweight terminal agent, and not locked to OpenAI: point it at any compatible provider or a local model through its config.
- **[forgecode](https://github.com/tailcallhq/forgecode)** — pair programmer across 300+ models (Claude, GPT, Grok, DeepSeek, Gemini and the rest), with model choice as the central feature rather than a settings page.
- **[kimi-cli](https://github.com/MoonshotAI/kimi-cli)** — one binary, no Node, millisecond startup; sub-agents, screen-recording input, MCP servers the agent configures itself. A free alternative on open Kimi models.
- **[openinterpreter](https://github.com/openinterpreter/openinterpreter)** — relaunched as a coding agent for open models: run it locally and code against an open model instead of a cloud API.
- **[pi](https://github.com/earendil-works/pi)** — agent toolkit with a unified LLM API, agent loop, TUI and its own coding-agent CLI.
- **[oh-my-pi](https://github.com/can1357/oh-my-pi)** — `pi` with an IDE wired in, and the section's answer to agents that edit code like it is plain text. Renames go through the language server (`workspace/willRenameFiles`), so re-exports, barrel files and aliased imports are updated before the file moves. It attaches a real debugger instead of sprinkling print statements — lldb on a segfaulting binary, dlv on a hung Go service, debugpy on a wedged Python process. Persistent Python and Bun kernels can call back into the agent's own tools, and stream rules abort the response mid-token when the model goes off-script and retry from the same point rather than taxing every turn with another instruction.

## Orchestration and agent fleets

- **[orca](https://github.com/stablyai/orca)** — an ADE for a fleet of parallel agents: run any coding agent on your own subscription, switch models, desktop / mobile / VPS.
- **[traycer](https://github.com/traycerai/traycer)** — runs several agents in parallel with shared memory across different models and providers, with model switching inside one chat and agent-to-agent handoff.
- **[background-agents](https://github.com/ColeMurray/background-agents)** — open-source background coding agents; a self-hosted take on Codex/Cursor background jobs.
- **[oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode)** — teams-first multi-agent orchestration for Claude Code: agent teams, hooks and HUDs rather than one agent with a longer leash. [oh-my-codex](https://github.com/Yeachan-Heo/oh-my-codex) is the same treatment for Codex.
- **[paperclip](https://github.com/paperclipai/paperclip)** — an app for managing the agents you run at work, when "which agent is doing what right now" stops being answerable from memory.
- **[LoopX](https://github.com/huangruiteng/loopx)** — the section's other axis: everything above spreads work across agents *at one moment*, this one holds one objective together *across weeks*. The durable state — goal, gates, todos, scope, evidence, quota — lives outside the agent, and Codex, Claude Code or Cursor execute one bounded turn at a time and write back evidence and a handoff before the next tick. When human judgement is needed it asks a concrete question and stops instead of spending the next slice. Installs as a single dependency-free Python CLI: `loopx connect` in the project root, `/loopx <task>` inside Claude Code. Useful when a task outlives the session it started in — a multi-day migration, an issue-and-review loop, a benchmark run — and the answer to "where were we" cannot be a compacted chat.

## Web, research and monitoring

Everything that lets the agent reach outside your codebase.

- **[wigolo](https://github.com/KnockOutEZ/wigolo)** — local MCP web layer: search / fetch / crawl / extract / research from one server, multi-engine search with rank fusion and on-device rerank. No API keys, no per-query billing.
- **[ego-lite](https://github.com/citrolabs/ego-lite)** — a browser for coding agents that *shares your logged-in state*, so the agent automates the web under your sessions without fighting you for the profile. Zero config.
- **[chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp)** — the official one: a real browser with a debugger, so the agent reads the console, the network tab and performance traces and reproduces the bug itself instead of trusting your retelling.
- **[vercel-labs/agent-browser](https://github.com/vercel-labs/agent-browser)** — the plain one, and the cheap default: a browser automation CLI where the agent opens a page, gets interactive elements back as refs and clicks them. `snapshot -i` returns the buttons, links and inputs instead of the whole DOM, which is the difference between a readable page and a context window full of markup. No shared profile, no debugger — reach for it when the agent just needs to go and click something.
- **[Agent-Reach](https://github.com/Panniantong/Agent-Reach)** — one CLI for reading and searching Twitter / Reddit / YouTube / GitHub / Bilibili / XiaoHongShu without API keys.
- 🥇 **[last30days-skill](https://github.com/mvanhorn/last30days-skill)** — an installable research skill: runs a topic across Reddit, X, YouTube, HN, Polymarket and the web and synthesizes a grounded summary with engagement signals. The radar behind this list runs on it, so the "install it and poke it" verdict is tested on myself.
- **[notebooklm-py](https://github.com/teng-lin/notebooklm-py)** — unofficial Python API plus an agentic skill for NotebookLM, including features the web UI does not expose.

## Beyond code: video, mobile, motion

Skills that give the agent a modality it did not have.

- **[claude-video](https://github.com/bradautomates/claude-video)** — `/watch` downloads a video, splits it into frames, transcribes it and hands the lot to the agent. A YouTube tutorial or a screen recording of a bug becomes readable input.
- **[agent-device](https://github.com/callstack/agent-device)** — hands on iOS and Android: the agent drives a real device or simulator for UI tests and automation. From the callstack (React Native) team.
- **[hyperframes](https://github.com/heygen-com/hyperframes)** — write HTML, get video; built to be driven from an agent pipeline.

## Model gateways and routing

- **[OmniRoute](https://github.com/diegosouzapw/OmniRoute)** — one endpoint over 39 provider pools and 460+ models, aggregating documented free tiers into a single live counter, with quota-aware fallback and token compression. Works with Claude Code, Cursor, Codex, Cline and Copilot.
- **[freellmapi](https://github.com/tashfeenahmed/freellmapi)** — stacks the free tiers of 28 providers behind one `/v1`.
- **[claude-code-router](https://github.com/musistudio/claude-code-router)** — route Claude Code at whatever model or provider you want.
- **[openai-oauth](https://github.com/EvanZhouDev/openai-oauth)** — use your existing ChatGPT account as an API credential.

## Integrations and credential brokering

- **[Corsair](https://github.com/corsairdev/corsair)** — one integration layer for agents: run your instance, connect the agent, and it reaches every integration **without ever seeing the credentials** — you gate what it may touch.
- **[DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)** — terminal, file operations (Excel/PDF/DOCX), diff editing and process control for Claude Desktop or any MCP client.
- **[aws/agent-toolkit-for-aws](https://github.com/aws/agent-toolkit-for-aws)** — official AWS bundle of MCP servers, skills and plugins: build and deploy to AWS without leaving the terminal.

## Design and UI quality

The most crowded niche on this list, and the one people argue about most: almost every one of these promises the agent will stop producing slop. They attack it from different ends — a skill that overrides its defaults, a design language it reasons in, a spec file that pins your identity, a searchable corpus it consults, a library of ready UI skills. Nobody has convincingly won yet, which is why there are nine of them — and why the one I recommend sidesteps the promise entirely and just shows you variants.

- ✅ **[prototype](https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype)** — the odd one out here, and the one I actually recommend: it does not try to give the agent taste, it makes the agent show you options. Ask "what should this look like" and it generates several radically different UI variations on one throwaway route, switchable from a floating bar, so you choose instead of arguing with a model about aesthetics. The other branch answers "does this state model feel right" with a tiny interactive terminal app. Throwaway by design — one command to run, no persistence, no tests, and an explicit ritual for folding the verdict back into real code and throwing the rest away.
- **[hallmark](https://github.com/Nutlope/hallmark)** — the anti-AI-slop skill: install it and the agent stops reaching for purple gradients. The breakout of July 2026 — 4.6k to 12.4k stars in a week.
- 🧪 **[taste-skill](https://github.com/Leonxlnx/taste-skill)** — the same promise, and the most popular skill in the category. I ran it on my own site: it produced three concepts on its own and the result was decent, though slop still shows through. Whether that was the skill or just a strong model, I could not fully separate — which is the honest state of this whole section.
- **[ui-ux-pro-max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)** — the reference-corpus end of the section: 67 UI styles, 161 palettes, 57 font pairings, 99 UX guidelines, 25 chart types and a body of reasoning rules the skill searches locally before the agent draws anything. Not a prompt that overrides the model's defaults but a database it looks things up in — which is a different bet on why the output is generic: not bad taste, no references. Installs as a Claude Code plugin or through `ui-ux-pro-max-cli`; works with Cursor and Windsurf too.
- **[impeccable](https://github.com/pbakaus/impeccable)** — not a skill but a design language your harness reasons in, so the taste survives across tools instead of living in one agent's prompt.
- **[design.md](https://github.com/google-labs-code/design.md)** — a `DESIGN.md` format that pins your visual identity as durable context, the way `AGENTS.md` pins conventions. Solves the other half of the problem: not "any taste" but *your* taste, the same on every run.
- **[ibelick/ui-skills](https://github.com/ibelick/ui-skills)** — skills for design engineers: the front-end and UI work itself, rather than the taste layer above it.
- **[google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)** — UI design skills built around the Stitch MCP server; works with Gemini CLI, Claude Code and Cursor.
- **[frontend-design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md)** — Anthropic's own answer to the same problem, shipped in the canonical skills repo. Worth trying before the third-party ones purely because it is what the model vendor thinks good front-end looks like.
- **[microsoft/flint-chart](https://github.com/microsoft/flint-chart)** — the narrow case nobody else covers: a visualization language that lets the agent produce legible charts from a human-editable spec, instead of one more unreadable matplotlib default.

## Output discipline

Skills that change the *form* of what the agent says, not its knowledge or its aesthetics.

- 🧪 **[i-have-adhd](https://github.com/ayghri/i-have-adhd)** — forces answer-first output: the conclusion up top, not buried under a wind-up.
- ❌ **[ponytail](https://github.com/DietrichGebert/ponytail)** — makes the agent lazy on purpose: think like the laziest senior on the team, "the best code is the code you didn't write". Changed nothing measurable on my projects, despite 80k+ stars. Possibly because I am already the laziest senior in the room.
- ❌ **[caveman](https://github.com/JuliusBrussee/caveman)** — the model talks like a caveman: "Me make. Done." Claims 60% token savings; measured savings are closer to 8%. Some people find the output easier to scan; for me it was not worth it.

## Directories and reference

Not "install and poke it" — reference material, kept in one place so the rest of the list can stay tools-only.

- **[anthropics/skills](https://github.com/anthropics/skills)** — the canonical Agent Skills repository.
- **[ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)** — the big directory of Claude skills.
- **[davepoon/buildwithclaude](https://github.com/davepoon/buildwithclaude)** — hub of skills, agents and commands.
- **[github/awesome-copilot](https://github.com/github/awesome-copilot)** — instructions, prompts and skills for GitHub Copilot.
- **[humanlayer/12-factor-agents](https://github.com/humanlayer/12-factor-agents)** — principles for agents that survive contact with production.
- **[anthropics/claude-cookbooks](https://github.com/anthropics/claude-cookbooks)** — recipes and notebooks.
- **[mattpocock/dictionary-of-ai-coding](https://github.com/mattpocock/dictionary-of-ai-coding)** — vocabulary for the field, which is moving faster than its terminology.

## How this list is maintained

A daily job sweeps GitHub Trending (all / Python / TypeScript) plus Reddit, X, Hacker News and Digg for agent tooling, deduplicates against everything already collected that week, and applies the two gates at the top of this page. Once a week the survivors are written up as a digest for [@fastnewsdev](https://t.me/fastnewsdev), and this list is the accumulated residue of those digests.

Three consequences worth stating plainly:

- **A star floor, but no star counts.** 500 stars is a threshold for getting in; after that the number is noise. Counts rot within days and turn a list into a leaderboard. Where a number appears in prose it is dated, because the velocity was the story.
- **Popularity is a floor, not a reason.** Clearing 500 stars gets a tool considered, nothing more. Several very large repositories are deliberately absent: agent-building frameworks, model releases, protocol politics, domain-specific MCP servers, and hubs whose content is other people's lists.
- **The radar sees things before this list does.** Interesting tools spend weeks below the floor, and some die there. The weekly digest covers them at day zero; this list waits.

Entries are dropped when a project is archived or absorbed, not when it stops trending.

## Contributing

Found something the radar missed? See [CONTRIBUTING.md](CONTRIBUTING.md). The bar is the same one at the top of this file: what does a developer do differently tomorrow because this exists — and has anyone but the author actually run it?

## License

[CC0 1.0 Universal](LICENSE) — to the extent possible under law, the maintainers have waived all copyright and related rights to this list.
