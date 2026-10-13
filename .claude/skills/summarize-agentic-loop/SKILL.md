---
name: summarize-agentic-loop
description: >-
  Summarizes an edition of The Agentic Loop, PulseMCP's bi-weekly newsletter on
  agentic engineering, AI agents, and the Model Context Protocol (MCP), into a
  fact-checked one-page briefing for a busy LSU ISDS student, ending with
  takeaways for class discussion and career prep. Use it whenever the user asks
  to read, summarize, recap, or get the highlights or takeaways of The Agentic
  Loop or the PulseMCP newsletter: the latest edition by default, or a specific
  past edition named by number (for example Agentic Loop 001), publication date,
  title, or pulsemcp.com/posts link. Use it even for casual asks like "what's new
  in the agentic loop?" Not for the older Weekly Pulse issues published before
  May 2026.
allowed-tools: WebFetch(domain:www.pulsemcp.com)
---

# Agentic Loop Summarizer

Turn one edition of *The Agentic Loop* into a short, fact-checked briefing for a busy LSU ISDS student who reads the briefing *instead of* the full newsletter. Because the reader won't check the original, every name, number, and claim must come from the edition itself, and the takeaways should help the student in class discussions and in preparing for a career in information systems.

Write as a precise AI-industry analyst: professional, concrete, plain English, no hype or filler.

These instructions work in Claude Code and in Claude chat. "Fetch" means your web fetch tool (WebFetch in Claude Code, web fetch in Claude chat).

## About the newsletter

- **The Agentic Loop** is published by PulseMCP (signed "Mike and Tadas") about every two weeks. Agentic Loop 001 came out on May 4, 2026. Earlier issues were called **Weekly Pulse**; this skill does not cover them.
- **Archive (the index to trust):** `https://www.pulsemcp.com/posts` lists editions newest first with labels like `Agentic Loop 002 • May 20, 2026`, each linking to its edition page. The same page also lists `Weekly Pulse NNN` issues and "Learn More" posts (handbooks, playbooks, guides). Neither is an Agentic Loop edition.
- **Edition pages:** `https://www.pulsemcp.com/posts/newsletter-...` hold the full text, currently an opening essay followed by a "Field Notes & Good Links" section of linked items. The page shows the title and date but *not* the edition number, so take the number from the archive.
- **Landing page:** `https://www.pulsemcp.com/newsletter` shows only a cut-off teaser of the latest edition, a "Read the full edition" link, and the next edition's date. Never summarize from it: the teaser is a fragment, and a briefing built on it misses most of the edition.
- Ignore page chrome wherever it appears: subscribe boxes ("Subscribe to The Agentic Loop", "Thanks for subscribing!"), reCAPTCHA text, navigation, author cards, and related-post lists.

## Workflow

### 1. Identify the requested edition

Work out which edition the user wants:
- **Nothing specific** ("latest", "new", "what's in the agentic loop?"): the most recent edition.
- **An edition number** ("Agentic Loop 001", "issue #2"): that number.
- **A date** ("the May 20 edition"): the edition published on that date.
- **A title or topic** ("the tokenmaxxing one"): the edition whose title matches.
- **A link** to a `pulsemcp.com/posts/...` page: that edition. Still look it up in the archive to get its number.

When the skill is run on demand as a slash command (for example `/summarize-agentic-loop 001` or `/summarize-agentic-loop May 20, 2026`), treat whatever follows the command as the request. With nothing after it, summarize the latest edition.

### 2. Look the edition up in the archive

Fetch `https://www.pulsemcp.com/posts` and ask for every entry labeled "Agentic Loop": its label, date, title, and link. Then:
- Pick the requested edition. "Latest" means the highest edition number.
- Note its **edition label**, **publication date** (write it as `May 4, 2026`), and **URL**. Treat the archive's title as provisional: the archive often changes a title's capitalization, so take the final title from the edition page in step 3.
- If the request matches no Agentic Loop edition, matches more than one, or points to a Weekly Pulse issue, stop and follow [When the request can't be summarized](#when-the-request-cant-be-summarized). Do not guess.

If your fetch tool refuses the archive URL because that URL hasn't appeared in the conversation yet (Claude chat can do this), search the web for `PulseMCP Agentic Loop newsletter posts` and fetch the pulsemcp.com link from the results. If the archive still can't be read, fall back to the landing page's "Read the full edition" link (for the latest edition) or the user's link, and leave the edition number out rather than guess it.

### 3. Read the full edition

Fetch the edition URL with this prompt, so every run collects the same facts:

> Extract a complete fact sheet of this newsletter edition, ignoring site chrome (subscribe boxes, reCAPTCHA, navigation, author cards, related posts). Give: (1) the title and publication date exactly as printed; (2) the central argument of the opening essay in 2-3 sentences, plus every named product, company, model, person, and number, with what the edition says about each; (3) every section heading in order and, under each, every bulleted item: its subject, a one-line factual description of what the edition says about it, and the link domain(s). Use short quotes only. Do not add anything that is not on the page.

If your fetch tool returns the page text instead of answering a prompt, build the same fact sheet yourself from that text.

Check that the fact sheet covers the whole edition: the opening essay *and* every item in each section. If it looks cut off, fetch again and ask only for the missing part. The fact sheet is your only source. Never fill gaps from memory, search results, or the landing-page teaser, because the student will treat every line of the briefing as fact.

### 4. Draft the briefing from the template

Read `assets/summary_template.md` from this skill's folder and fill in every placeholder:
- **Header:** copy the template's first four lines exactly, changing only the bracketed parts. The briefing must start with the line `# Agentic Loop Executive Summary`, followed by the `**Edition:**`, `**Published:**`, and `**Source:**` lines. Use the edition label from the archive, the title exactly as the edition page's headline prints it (not the archive's version), the edition's publication date (not today's date), and the edition page URL (never the `/newsletter` landing page).
- **🚀 Executive Summary:** 2-3 sentences, never more, on the edition's central argument and why it matters. When an edition makes several points, combine them into fuller sentences or move the extra facts into the bullets below; four short sentences break the format the student expects to skim.
- **🛠️ Strategic Tech & MCP Updates:** the 3-4 most significant concrete items (tools, products, model releases, standards changes, or notable adoption news), one sentence each, led by the bolded name. Prefer specific, named developments over general commentary.
- **💡 Key Takeaways for an LSU ISDS Student:** exactly two numbered takeaways, *For class discussion* and *For your career*, each one or two sentences and tied to a specific point in the edition. These are your analysis, so make them useful, but don't claim anything the edition doesn't support.
- Delete the italic guidance lines and every square-bracket placeholder. Keep the headings, emoji, order, horizontal rules, and footer exactly as they appear in the template.

Use the full template however the request is phrased ("quick rundown", "just the takeaways"). The format is already brief, and the same layout every time is what makes the briefing quick to scan edition after edition.

### 5. Adversarial review

Before replying, check the draft line by line against the fact sheet:
1. Every name, number, date, quote, and claim appears in the fact sheet. Fix or delete anything that doesn't.
2. Each claim is credited to the right company or person. For example, don't credit one company with work the edition attributes to another.
3. The takeaways follow from the edition and don't overstate it.
4. The layout matches the template: the `# Agentic Loop Executive Summary` title and three header lines (with the title capitalized as on the edition page), the same headings in the same order, an executive summary of no more than three sentences, 3-4 update bullets, exactly two takeaways, the footer, no leftover placeholders, and nothing added before or after.

### 6. Deliver

Reply with the finished briefing only: no preamble, and no notes or offers after the footer. If the user asked for several editions, give one complete briefing per edition, newest first.

## When the request can't be summarized

Reply in two or three plain sentences instead of the template, and never invent an edition:
- **A Weekly Pulse issue, or a date before May 4, 2026:** explain that it's from the newsletter's earlier Weekly Pulse era, which this skill doesn't cover, and list the available Agentic Loop editions (label, date, title).
- **No matching edition** (for example, a number that hasn't been published yet): say so, list the available editions, and give the next edition's date from the landing page (fetch it if you haven't).
- **Several matches** (for example, "the May edition"): list the matching editions and ask which one the user wants.
- **The site can't be reached:** retry once. If it still fails, say the edition couldn't be retrieved right now and stop. Don't summarize from memory or search snippets.

## Supporting files

- `assets/summary_template.md`: the required output format. Read it before every draft.
