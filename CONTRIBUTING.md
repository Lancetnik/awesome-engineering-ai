# Contributing

Suggestions are welcome. This list is curated rather than collected, so most of these rules are about what gets *rejected*.

## The bar

Two gates. A submission has to clear both.

**1. What does a developer do differently tomorrow, at their keyboard, because this exists?**

If the honest answer is "nothing yet, but it's interesting" — it does not go in. That is not a judgement of the project; it is the scope of the list.

**2. At least 500 stars.**

Below that, submissions are closed — including excellent ones, including your own. The floor exists because a tool nobody outside its author has run cannot be recommended to anyone, and because most sub-500 repositories in this space are abandoned within a month. Sitting at 480 is not a rejection, it is a "not yet": resubmit when it clears.

For the few entries that are products rather than repositories, the equivalent is a public track record — a real user base, not a landing page.

## Accepted

- Agent skills, MCP servers, plugins, CLIs and harnesses you install and use **with** a coding agent (Claude Code, Cursor, Codex, Gemini CLI, opencode, …).
- Features and layers on top of daily tools, when they change how you work.
- Workflow methods with a concrete installable implementation (spec-driven development toolkits, for example).

## Rejected

- **Frameworks for building agents** — LangChain, AG2, AutoGen, CrewAI-the-framework, agent harness SDKs. Different audience: you are writing an agent, not using one.
- **Domain MCP servers** — stock tickers, CRMs, crypto, SEO dashboards. Endless, and each is relevant to a handful of people.
- **Model releases, pricing news, protocol politics, security incidents.** Real news, wrong list.
- **Consumer AI products** and app builders that are not part of a coding workflow.
- **Listicles, courses, glossaries and directories** — with the single exception of the [Directories and reference](README.md#directories-and-reference) section, which is deliberately short.
- **Repositories with no description**, where what the tool does cannot be established from the README.
- **Anything under 500 stars**, however good. See the bar above.

Popularity is a floor, not an argument. Clearing 500 stars gets a tool considered, nothing more — several 100k+ star repositories are absent on purpose.

## Format

One line per entry:

```markdown
- **[name](https://github.com/owner/repo)** — what it does, in one sentence, and why it is different from its neighbours in the section.
```

- Say what the tool **does**, not what it claims to be. "MCP server that gives the agent a real browser with a debugger" beats "next-generation AI-powered browser automation platform".
- Position it against the section: most categories here already have three or four tools, so the useful part of a description is the difference.
- No star counts, no badges, no marketing adjectives. Stars are checked at review time and never written into the list.
- Verdict marks (🥇 ✅ 🧪 ❌) are personal and are only added by the maintainer after actually running the tool. Do not add one to your own submission.

## Submitting

Open an issue or a pull request with:

1. The link.
2. One sentence on what it does.
3. One sentence answering the bar question — what you now do differently.
4. The current star count, so the floor can be checked without a round trip.
5. Whether you have actually run it (this changes nothing about acceptance, but it changes how the entry is written).

Self-promotion is fine, provided the bar question has a real answer. Say that it is yours.
