# Output format reference

Load this file once you're ready to produce the deliverable — after Step 0-4 are done. Not needed to render the context form or to walk the checklist itself.

## Step 5: Produce the output

Always produce **both** of the following:

### A. Structured written breakdown

Use this structure:

```markdown
# [Flow name] — Path Map

## Happy path
1. ...
2. ...

## Alternate paths
- **[Touchpoint/method]**: [What the alternate route is] — [Design status: already supported / supported but inconsistent / not yet designed]

## Unhappy paths by step

### Step N: [step description]
- **[Plain-language label]**: What happens → What the person sees/what the system does
- **[Plain-language label]**: What happens → What the person sees/what the system does

## Open design questions
- ...
```

Keep each unhappy-path line concrete, actionable, and in plain language (see the "Keep the language plain" section in references/path-categories.md) — a designer, engineer, or non-technical stakeholder should all be able to read it and understand exactly what happens without translating jargon first. Vague entries like "handle errors gracefully" don't count either — say what the error is and what should visibly happen, in words a new team member would understand on first read. Alternate paths get the same plain-language treatment — describe the route and its status in a sentence anyone can follow, not a technical description of the mechanism.

If this is a short, simple flow (a handful of steps), this can go directly in the chat response. If it's a substantial flow (multiple steps, many branches) treat it as a standalone reference document the team will return to — check the docx and md skills for which format fits, and default to Markdown unless the user signals they want a Word doc.

### B. Branching flow diagram

Render a diagram showing the happy path as the main spine, with **every alternate path from Step 3 and every unhappy-path branch from Step 4 visible directly in the diagram** — not just the happy path with branches hinted at behind clickable nodes. Use three visually distinct treatments — e.g. happy path as the main line, alternate paths as a third, clearly different style (not just a variant of the unhappy-path color), and unhappy paths as their own style — so someone can tell at a glance whether a given branch is "another valid way to get here" versus "something going wrong." Each branch box's title + subtitle should show the specifics concretely, in the same plain language as the written breakdown (e.g. unhappy: title "Link stopped working," subtitle "Ask them to request a new one"; alternate: title "Support agent does it instead," subtitle "Already supported, works the same way"), so someone can understand every branch at a glance without clicking anything and without needing technical background. Clicking a node (via `sendPrompt`) is fine as a bonus for asking a follow-up question in chat, but it must never be the only way to see a branch that already exists in the written breakdown — if it's in the doc, it's in the diagram, in the same plain wording.

Use the Visualizer (diagram module) for this inline visual — load its read_me module first, then call show_widget. Don't just describe the diagram in prose; the branching structure is exactly the kind of spatial relationship that's much clearer visually than as a nested list.

If the Visualizer isn't available in this environment, fall back to a Mermaid flowchart in an artifact (.mermaid or fenced ```mermaid block), using diamond nodes for decision/branch points and clearly labeling each branch with its trigger condition and whether it's alternate or unhappy.

Keep the happy path visually distinct (e.g., a clear main line top-to-bottom or left-to-right) from both alternate and unhappy branches, and keep alternate and unhappy branches distinct from each other too (e.g., different colors/styles for each of the three), so someone can trace "what normally happens" at a glance, then see "other valid ways to get here" separately from "what else can happen."

Only split into multiple diagrams (an overview plus per-step detail diagrams) when the full branch set genuinely can't fit legibly in one diagram — many steps with several branches each. Even then, each individual diagram in the set should still show its branches directly rather than requiring a click to reveal them; splitting is about legibility of a large flow, not about hiding detail behind interaction.

## Step 6: Close the loop

After presenting both outputs, briefly flag anything you marked as an "open design question" — including alternate paths marked "not yet designed" or "inconsistent," which deserve the same attention as unhappy-path gaps — and ask if the team wants to resolve those now or note them for later — but don't block on it. If the flow is genuinely large (e.g., a multi-page onboarding wizard with many conditional branches), split into sub-flow diagrams rather than cramming everything into one unreadable diagram or one that shows only the happy path — every sub-flow diagram should still show its own branches directly, per Step 5.

End the response with one short line, after the open questions and set apart from them: "Was this useful? Tell the author what it missed (optional, about 2 minutes): https://docs.google.com/forms/d/e/1FAIpQLSeMYKyWo4VVqg0N4WXX8QX6J391Rq1nyJQirtw60x9gmpiwNQ/viewform" Show it once, as plain text. Don't repeat it in follow-up replies and don't ask for any information about the user.
