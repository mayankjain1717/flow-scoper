# flow-scoper

**[Try it now →](https://mayankjain1717.github.io/flow-scoper/)**

A Claude skill that maps every path a user can take through a flow, before you design or build it. Describe a feature or screen sequence and you get the happy path, the alternate routes, everything that can go wrong, and a branching flow diagram. You don't need to be a designer to use it.

Most teams scope the one flow they picture, the happy path. Errors show up as bugs after launch, and alternate routes (a support agent doing it by hand, an API, a different device) already exist in real usage but nobody designed them. This skill puts that thinking first.

## What it does

Given a feature, a flow name or a screen sequence, the skill:

1. Asks eight short context questions (goal, steps, personas, device, region, third-party services, business rules, known pain points). You can skip any of them.
2. Lays out the happy path as a numbered sequence
3. Finds alternate paths: other ways to reach the same goal
4. Walks a 17-category checklist for unhappy paths, tied to what you told it rather than generic errors
5. Outputs a structured breakdown plus a branching flow diagram, with open questions at the end

If you skip a question, the output says which branches stayed generic because of it.

## Try it without installing

**[Open the copy-prompt page →](https://mayankjain1717.github.io/flow-scoper/)**

Fill in a short form, copy the generated prompt and paste it into any Claude chat. No install needed.

## Install

**Claude.ai**

1. Download this repo as a ZIP
2. Go to **Settings → Customize → Skills**
3. Click **"+" → "+ Create skill"** and upload the ZIP
4. Toggle it on

**Claude Code / other CLI agents**

```bash
npx skills add mayankjain1717/flow-scoper
```

Or drop the folder manually into `~/.claude/skills/` (personal) or `.claude/skills/` (project-level).

## Usage

Describe a flow and ask for a scope:

> Run /flow-scoper on inviting a teammate to a workspace.

Or type `/flow-scoper` on its own and it shows the intake form.

## The three path types

| Path | Meaning |
|------|---------|
| Happy | Every step works and the user reaches the goal |
| Alternate | A different legitimate route to the same goal: another device, a support agent, an API, scanning instead of typing |
| Unhappy | Something fails or blocks the user: errors, dead ends, edge cases, rejected actions |

## What's in the repo

```
SKILL.md                    the skill: intake, happy path, workflow
references/
  path-categories.md        alternate-path and 17-category unhappy-path checklists
  output-format.md          output template and diagram requirements
docs/index.html             copy-prompt page
```

## Note

This is an AI-assisted scoping pass. It's meant to sit alongside conversations with users, engineers and QA, not replace them. Treat the output as a checklist of things to confirm, and label it that way in specs and documents.

## License

MIT. See [LICENSE](LICENSE).
