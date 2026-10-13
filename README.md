# Agentic Loop Summarizer

**One sentence:** `summarize-agentic-loop` is a Claude agent skill that turns any edition of *The Agentic Loop*, PulseMCP's bi-weekly newsletter on agentic engineering, AI agents, and the Model Context Protocol (MCP), into a fact-checked, one-page briefing for a busy LSU ISDS student.

## Why it's a good skill

| Requirement | How this skill meets it |
| :--- | :--- |
| **Repeatable** | A new edition comes out about every two weeks, and the skill summarizes any of them (the latest, or one picked by number, date, title, or link) with the same steps and layout every time. |
| **Useful to a defined user** | A busy LSU ISDS student who wants to keep up with agentic AI without reading every full edition. Each briefing ends with one takeaway *for class discussion* and one *for your career*. |
| **Appropriately scoped** | It does one job: summarize one Agentic Loop edition. It declines the older *Weekly Pulse* issues and never invents editions that don't exist. |

## What's in the repo

```
.claude/skills/summarize-agentic-loop/
├── SKILL.md                     # frontmatter (name + trigger description) and step-by-step instructions
└── assets/
    └── summary_template.md      # supporting resource: the required output format
instructions.md                  # course project directions
```

`SKILL.md` covers when the skill applies (its description), how to find the requested edition, how to read the full edition and not just the landing-page teaser, how to fill in the template, an adversarial fact-check pass, and how to handle requests it can't fulfill.

## How to run it

### Claude Code (recommended: no setup)

1. Clone this repository and start Claude Code in its folder (`claude`). The skill loads automatically from `.claude/skills/`.
2. Run it on demand:
   - `/summarize-agentic-loop`: the latest edition
   - `/summarize-agentic-loop 001`: a specific edition by number
   - `/summarize-agentic-loop May 20, 2026`: a specific edition by date
3. Or ask in plain English, and the skill triggers on its own: *"What's new in the latest Agentic Loop newsletter?"*

### Claude chat (claude.ai or the desktop app)

1. Turn on **Settings > Capabilities > Code execution and file creation**.
2. Add the skill under **Customize > Skills**: compress the `summarize-agentic-loop` folder into a ZIP and upload it.
3. pulsemcp.com blocks Claude chat's built-in web fetch, so in Claude chat the skill reads the site in a browser window instead. It uses the Claude desktop app's built-in browser, or the [Claude in Chrome](https://support.claude.com/en/articles/12012173-get-started-with-claude-in-chrome) extension (paid plans). If neither is available, the skill explains how to set one up.

## Testing

Every automated test below was a fresh, headless Claude Code session with only this project skill installed. Apart from the slash-command tests, no prompt named the skill.

| Test | Result |
| :--- | :--- |
| **Triggering:** 9 requests that should use the skill and 8 look-alikes that shouldn't (e.g. "what is MCP", other newsletters, a Weekly Pulse issue), 2 runs each | **17/17 correct** |
| **Different inputs, run twice each:** latest edition (→ 002), "Agentic Loop 001", "the edition from May 20, 2026", and an edition link | Right edition every time. In the final round, 7 of 8 runs passed all 12 format checks; one ran to 4 summary sentences instead of 2-3. |
| **Edge cases:** an unpublished edition (003), a Weekly Pulse request, the slash command with and without an edition, a run without file-reading tools | All handled correctly. For 003, it says the edition isn't out yet and lists the real ones. |
| **Fact check:** an independent reviewer compared 8 briefings with the source editions | No wrong numbers, dates, or credits to the wrong company; 3 minor wording stretches |
| **Claude chat:** a real run in the Claude desktop app | Produced the correct Agentic Loop 002 briefing by reading pulsemcp.com in its own browser window |

Before this skill was reworked, the original version summarized only the landing-page teaser, so its "latest edition" briefing had no date and no named tools. Its description also hard-coded a stale date.

<details>
<summary><b>Example output 1: latest edition</b> (prompt: "what's new in the latest agentic loop newsletter? give me the rundown")</summary>

# Agentic Loop Executive Summary
**Edition:** Agentic Loop 002 — *The Tokenmaxxing Reckoning is Near*
**Published:** May 20, 2026
**Source:** [Read the full edition](https://www.pulsemcp.com/posts/newsletter-tokenmaxxing-reckoning-is-near)

---

## 🚀 Executive Summary
Many companies have fallen into "tokenmaxxing," measuring AI-enabled productivity by token spend alone. Token-burning firms and genuinely AI-empowered ones look alike from the outside, so the edition expects the pretenders to be separated from the real successes in the coming months. It also predicts that tinkerers will swap cheaper models and harnesses into work that doesn't need frontier models like Opus 4.7 or GPT 5.5.

## 🛠️ Strategic Tech & MCP Updates
- **Cheaper near-frontier models:** The edition points to Cursor Composer 2.5 and Google Gemini 3.5 as near-frontier releases that are "10x cheaper," supporting its case for swapping in cheaper models.
- **Anthropic subsidy change:** Anthropic pulled back from subsidizing token costs for individuals using Claude Max plans programmatically, which adds pressure to optimize spend.
- **MCP Apps and Skybridge:** The edition argues HTML is becoming the output format for agentic work, and says Alpic's Skybridge framework powers over 10% of apps in the Claude and ChatGPT MCP App stores.
- **Vendor-neutral control planes:** The edition flags MCP Gateway and LLM Gateway-style control planes as a category to watch, because enterprises want to avoid single-provider lock-in.

## 💡 Key Takeaways for an LSU ISDS Student
1. **For class discussion:** The edition says token spend is a poor productivity metric and that software vendors are shifting from per-seat to usage-based pricing, so ask what metrics should measure the business value of AI and how pricing changes affect IT budgeting.
2. **For your career:** The edition expects cost-conscious teams to swap cheaper models into work that doesn't need frontier models and to watch vendor-neutral gateways. Learning to compare model cost against task needs and to work with MCP-based tooling is therefore worth building.

---
*Generated by the Agentic Loop Summarizer Skill. Verified via adversarial review against source material.*
</details>

<details>
<summary><b>Example output 2: a different input</b> (prompt: "Can you summarize Agentic Loop 001 for me? I missed the first edition after they rebranded.")</summary>

# Agentic Loop Executive Summary
**Edition:** Agentic Loop 001 — *Mission Accomplished, We're Rebranding to The Agentic Loop*
**Published:** May 4, 2026
**Source:** [Read the full edition](https://www.pulsemcp.com/posts/newsletter-mission-accomplished-rebranding-agentic-loop)

---

## 🚀 Executive Summary
The Weekly Pulse is now The Agentic Loop. The authors argue that MCP, which launched in 2024, has outgrown its early days, when Claude Desktop was the only client, and is here to stay, with 500+ clients and "many thousands of servers." Coverage will still include MCP, but it will now focus on practitioners and leaders adopting agentic AI, and the newsletter will publish bi-weekly.

## 🛠️ Strategic Tech & MCP Updates
- **Autonomous PR approval:** Intercom reports that 19% of its pull requests are auto-approved with no human in the loop.
- **Background coding agents:** Stripe Minions and Ramp Inspect run coding agents in the cloud, and the edition covers the infrastructure they require and a "build vs. buy" vendor landscape from Ona.
- **Triggers renamed Events in MCP:** An experimental MCP extension lets servers proactively message connected clients, and Claude Code's Channels implementation came first.
- **Organizations adopting MCP:** Google (Workspace MCP servers), X (official MCP server), Salesforce (hosted MCP servers, generally available), Pinterest (internal MCP architecture writeup), and Zoom (partnership with Anthropic).

## 💡 Key Takeaways for an LSU ISDS Student
1. **For class discussion:** Intercom's 19% of PRs auto-approved with no human in the loop raises a governance question: what controls and accountability should exist when agents ship code without human review?
2. **For your career:** Intercom, Every.to, and Ramp all keep their agents' artifacts (Plugins, agent definitions, Skills) in git, and the Agent Skills guidance says to "Start from real expertise." Learning to write and version-control Skills and to design MCP servers are practical skills to build.

---
*Generated by the Agentic Loop Summarizer Skill. Verified via adversarial review against source material.*
</details>
