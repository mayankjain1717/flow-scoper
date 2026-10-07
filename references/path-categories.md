# Path categories reference

Load this file after Step 0 and Step 1/2 are done — it's not needed to render the context form, only to actually walk the checklist once you have a happy path to check.

## Step 3: Map alternate paths

An alternate path is **not a failure** — it's another legitimate way someone reaches the same goal, just not the one route the team had in mind. This is easy to miss precisely because nothing is broken: the team designs the one screen-based flow they pictured, and doesn't notice that a support agent, an API, a bulk-import tool, or an entirely different device already gets someone to the same outcome a different way, often without anyone deciding that on purpose. An alternate path nobody has actually designed for is effectively an unhappy path in disguise — it just doesn't announce itself with an error message.

For the flow as a whole (some alternate paths bypass the entire sequence) and for individual steps (some alternate paths swap out just one step), check each of these — using the Step 0 answers to make them concrete rather than generic, the same way Step 4 does for unhappy paths:

- **Different touchpoint / channel** — same goal reached through a different surface: a support/CS agent doing it on the person's behalf, an API or MCP-style integration bypassing the UI entirely, a different device or app in the same product suite, a phone call or chatbot instead of the screen flow. Ground this in Step 0's platform and external-dependencies answers — if there's an API/MCP surface or a support tool, name it specifically.
- **Different actor** — someone other than the primary persona completes the step: an admin or teammate acting on another user's behalf, a delegate, an automated agent doing it for them.
- **Different method for the same step** — e.g. manual entry vs. bulk/CSV import vs. automated sync; scanning vs. typing; voice vs. text — same outcome, different mechanics.
- **Different order** — valid steps taken out of the order the team assumed, without anything failing (e.g. setting up a payment method after the first order instead of before it).
- **Skipping optional steps** — reaching the goal via a shorter valid route because some steps turn out to be optional, not required.
- **Pause and resume elsewhere** — legitimately starting on one touchpoint and finishing on another (e.g. start on mobile, finish on desktop) — distinct from "concurrency/stale state" below, which is a failure; this is a valid continuation, not a conflict.

For each alternate path found, write one line: what the route is, and its design status — **already supported and consistent** with the main happy path, **supported but inconsistent** (gets there, but the experience differs in a way that's probably unintentional), or **not designed for at all**. Flag anything in the last two buckets as an open design question — those are the ones worth the team's attention; a path that's already well-supported doesn't need a redesign, just a mention so the team knows it exists.

Don't force this — a simple, single-touchpoint flow with no support/API/bulk alternative genuinely may have no alternate paths worth noting. The goal is catching real blind spots, not manufacturing alternates that don't exist.

## Step 4: Systematically surface unhappy paths

**First, filter which categories are even in play for this flow — before checking any individual step.** Seventeen categories is deliberately broad so this skill works for any kind of product, but most flows only ever trigger a subset of them. Using the Step 0 answers (main actions, platform, external dependencies), rule out entire categories up front if they structurally cannot apply to this flow — don't carry them forward into the step-by-step pass at all. For example: a flow with no physical/warehouse component can never hit "physical/digital mismatch," so drop it entirely rather than re-checking it against every step and writing "not applicable" each time. This keeps the output focused on what's actually useful for the flow being mapped, instead of a 17-item checklist dutifully filled out regardless of relevance.

The first 8 are close to universal — most flows should at least consider them:

- **Invalid input** — user enters something malformed, out of range, or in the wrong format
- **Missing input / empty state** — user has nothing yet (empty cart, no results, first-time use)
- **Permission / auth** — user isn't logged in, lacks access, session expired mid-flow
- **System / network failure** — timeout, server error, offline, third-party API down
- **Concurrency / stale state** — the thing the user is acting on changed or was deleted by someone/something else since the screen loaded
- **User abandonment / interruption** — user leaves, backgrounds the app, or closes the tab partway through
- **Business-rule rejection** — the action is well-formed but disallowed by a rule (insufficient funds, quota exceeded, duplicate entry)
- **Ambiguous or reversed intent** — user wants to undo, go back, or realizes they made a mistake after committing a step

The rest apply only when the flow has the relevant characteristic — check Step 0 for the signal noted with each one:

- **Accessibility / situational constraints** — the person can't complete this step the way it's designed, even with no bug involved: relying on a screen reader or keyboard-only navigation, low digital literacy, an old device or slow/limited connection, or simply being stressed or distracted mid-task. Distinct from "system/network failure" — nothing is broken on the backend, the interface just doesn't accommodate how this person is actually using it. *Broadly relevant to almost any user-facing flow; drop only for pure back-office/system-to-system flows with no human in the loop.*
- **Localization / regional differences** — the product hits a legitimate regional context it doesn't handle: date/number/currency formatting, timezones and daylight saving, right-to-left layout, or a translation that doesn't exist yet. Distinct from "invalid input" — the person didn't do anything wrong, the product just wasn't built for their region yet. *Signal: Step 0 geographic scope indicates multi-region now or planned.*
- **Security / malicious use** — this isn't a legitimate user making a mistake or hitting a rule; it's someone deliberately attacking the flow: credential stuffing a login, guessing emails/codes on an auth step, scripted repeated attempts, card testing on a payment form, or abusing a referral/signup bonus. Distinct from "business-rule rejection" — a real user who fat-fingers their password five times and a bot trying five thousand guesses hit the same "too many attempts" trigger, but need different responses: the real user gets a helpful, specific message, while the attacker gets something deliberately vague or silent so the response doesn't hand them useful feedback. *Signal: flow touches auth, payments, or anything with cash-value abuse potential (referrals, quotas, bonuses).*
- **Data sync / integration conflicts** — two systems each think they're the source of truth and disagree, without either being simply "behind." E.g. a sales channel says 10 units in stock, the warehouse system says 7 — neither is stale, they've genuinely diverged. Distinct from "concurrency/stale state," which assumes one system is behind the other and just needs a refresh; this is two systems that are each internally consistent but disagree with each other. *Signal: flow involves two-way sync with an external system (inventory, calendar, CRM, accounting).*
- **Automation vs. manual trigger conflicts** — a process can run automatically or be manually triggered, and the two collide: automation fails silently while the person assumes it worked, or a manual trigger fires while an automated run is already in progress, causing duplication or a race. *Signal: flow explicitly supports both an automatic and a manual path to the same outcome.*
- **Physical / digital mismatch** — the system's record and physical reality disagree (miscount, damage, a misplaced item), or a physical device involved in the step fails mid-task (scanner, printer, label maker, sensor). *Signal: flow involves a warehouse, field operation, point-of-sale, or any hardware step — skip entirely for purely digital flows.*
- **Multi-party / external-partner dependency** — a dependency has its own rules, SLAs, or capacity your system doesn't control — a carrier missing an SLA, a vendor running out of capacity. Distinct from a plain "system/network failure" API dependency: the fix isn't retry/timeout handling, it's escalation, rerouting, or a business-level fallback. *Signal: flow depends on an external business partner (carrier, vendor, marketplace), not just a technical API.*
- **AI-agent / autonomous action failures** — an AI agent (chatbot, MCP-connected tool, autonomous workflow) is taking actions on the person's behalf, not just answering: it misreads intent and takes the wrong action, needs to be undoable, hits a usage/rate limit mid-task, or acts outside the scope it should be allowed to touch. *Signal: flow involves an AI agent or assistant that can take actions, not just retrieve/display information.*
- **Legal / compliance / consent state** — distinct from both "permission/auth" (access rights) and "business-rule rejection" (business logic): the person's legal or consent status blocks or changes the flow. Their consent went stale because the privacy policy changed and they haven't re-accepted; a data-residency rule blocks the action for their region; they've triggered a right-to-be-forgotten or data-deletion request while a transaction is in progress; a required disclosure hasn't been accepted yet. *Signal: flow touches personal data, payments, or anything with regulatory exposure (GDPR/CCPA-style consent, financial compliance).*

For each applicable category at each step, write one line: what triggers it, and what the system should do about it (error message, fallback state, retry, redirect, etc.). If the "right" resolution is a genuine design decision rather than an obvious default, flag it as an open question instead of inventing an answer — that's more useful to a design team than a confident guess.

Use the Step 0 answers to make these specific rather than generic: named external dependencies belong in "system/network failure" (e.g. "Stripe times out" not "payment fails"), named business rules belong in "business-rule rejection" (e.g. "monthly export quota exceeded" not "some limit is hit"), and named personas should surface persona-specific branches where they'd genuinely differ (e.g. a guest checkout has no saved payment method to fall back on; a logged-in member does).

Handle localization based on the Step 0 geographic-scope answer, using any named regions (e.g. "US + India + China") to make branches specific — each region's currency, formats, languages and scripts, payment methods, and privacy or data-residency rules: if the org has no expansion plans, skip this category like any other that doesn't apply. If they're single-region today but planning to go global, still surface the relevant localization branches — just label them clearly as forward-looking (e.g. under "Open design questions" or flagged "future: multi-region") rather than treating them as things that must be fixed before shipping the current, single-region version.

Don't pad the list — a login step probably doesn't have a "concurrency" issue, and a "view a static page" step probably has no unhappy paths at all. The goal is real coverage, not a checklist filled in by force.

## Keep the language plain

These category names are for organizing your own analysis while you walk the checklist — they are **not** meant to appear verbatim in what you show the user. Anyone on the team — not just engineers — should be able to read the output and immediately understand it. Translate every category and every trigger/response into a plain sentence, the way you'd explain it out loud to a teammate who isn't technical:

| Instead of this jargon | Write this |
|---|---|
| "Concurrency / stale state" | "Someone else changed or deleted it first" |
| "Business-rule rejection: quota exceeded" | "Not allowed because they've hit their monthly limit" |
| "Auth failure / session expired" | "They got logged out partway through" |
| "System/network failure: third-party API timeout" | "The system couldn't reach [named service] in time" |
| "Invalid input: malformed format" | "They typed it in a way the form doesn't recognize" |
| "Endpoint returns 404 / link invalidated" | "The link stopped working" |
| "Accessibility / situational constraint: screen reader incompatible" | "Someone using a screen reader can't tell what this button does" |
| "Localization: currency/date format mismatch" | "The price or date doesn't display correctly outside the US" |
| "Security: credential stuffing / brute force detected" | "Someone's trying a lot of password or code guesses in a row" |
| "Data sync conflict: source-of-truth divergence" | "Two systems disagree on the number, and neither is behind" |
| "Automation/manual trigger race condition" | "The automatic version ran at the same time someone did it by hand" |
| "Physical/digital mismatch: inventory discrepancy" | "What's on the shelf doesn't match what the system shows" |
| "Multi-party dependency: partner SLA breach" | "The carrier/vendor didn't deliver on their side in time" |
| "AI-agent scope violation / misread intent" | "The assistant did something the person didn't actually ask for" |
| "Legal/compliance: consent stale under new policy version" | "They need to agree to the updated terms before continuing" |

Avoid words like *endpoint, API, payload, null, timeout, auth, session, concurrency, race condition, validation* unless the team you're writing for genuinely uses that vocabulary day to day (ask in Step 0 if unsure, or default to plain). A category name can still head the line as a short label if it's already plain English ("Missing input," "User changes their mind") — the rule is about avoiding unnecessary technical jargon, not about banning short labels entirely.
