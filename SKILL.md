---
name: flow-scoper
description: Maps every happy path, alternate path, and unhappy path (edge cases, errors, failure states) for a user flow before or during prototyping, producing a structured breakdown plus a branching flow diagram. Use this whenever someone describes a user flow, feature, or screen sequence and is heading into design or prototyping — even if they don't say "happy path" or "unhappy path" explicitly, and even if they invoke the skill directly (e.g. "/flow-scoper") with no flow description at all — in that case, show the context-gathering form immediately rather than waiting for more text. Also trigger for requests to think through edge cases, error handling, failure states, what could go wrong, validation, empty states, alternate routes or touchpoints, or a UX/flow review of a feature. Also trigger when someone wants to scope a feature or flow before building it. Good for PMs, founders, engineers, and designers scoping a flow before wireframes or code.
---

# Flow Scoper

Design teams and prototypers usually design the happy path first and only discover unhappy paths (errors, dead ends, edge cases) once real users or QA hit them — and separately, they often only design for the *one* touchpoint they had in mind, missing that people already reach the same goal through a support agent, an API, a different device, or some other route nobody planned for. This skill front-loads both kinds of discovery.

**Everything this skill produces should be grounded in the context gathered in Step 0, not generic patterns.** Tie every branch back to something the user actually told you — a named persona, platform, dependency, or business rule — rather than a hypothetical one.

## Performance note: render the form first, read ahead second

**Step 0 is everything you need to respond immediately.** Do not read `references/path-categories.md` or `references/output-format.md`, and do not plan out Steps 3-6, before rendering the Step 0 form — that reference material is only relevant once the person has actually answered, and reading it early just adds delay before they see anything. Treat "show the form" as the first and only action on trigger; load the reference files afterward, once you're past Step 2 and actually walking the checklist.

## Step 0: Gather context

**Handle bare invocation first.** If the skill is invoked with no flow described at all — e.g. just the skill name with no accompanying task, or something as thin as "help me map a flow" — don't wait for a follow-up message and don't just ask "what flow?" in plain text. Immediately show the full context-gathering form (see below), with one extra field at the top using the exact wording: **"What flow or feature are we mapping today?"** (short text, e.g. "checkout," "reset password," "inviting a teammate"). Treat this the same as any other Step 0 answer — everything gets submitted and processed together in one round trip.

Before mapping anything, always ask for this context up front — a path map built without it tends to read as generic (every step gets the same boilerplate errors) instead of specific to the actual product and users.

**Use this exact wording every time — do not paraphrase or rephrase between sessions.** People using this skill across different flows should see the same, consistent set of questions, in the same product-and-design vocabulary, every time. The line after each question is context for you, not something to read aloud or include in the form.

1. **"What's the goal of this flow, and what does success look like for the user?"**
   *(Intent and outcome — not the mechanics of how they get there.)*
2. **"Walk me through the main steps a user takes, in order, to complete this flow."**
   *(The actual sequence, from the user directly — don't infer or guess this yourself if they can give you the real one. Getting it firsthand matters most for flows with a branch point baked into the "normal" path itself, like "scan a QR code or type a code manually," or a multi-party step like an approval with more than one approver — a guessed sequence is likely to miss those.)*
3. **"Who is this for — one type of user, or a few different personas? Tell me anything you know about them: demographics, goals and needs, pain points, personality traits."**
   *(Different personas often need different unhappy-path or alternate-path branches at the same step. If using pills for this question, use exactly: "New user," "Returning user," "Admin/Account owner," "Other" — multi-select, since a flow can involve more than one. Pair the pills with a free-text field for the richer detail, and make clear it is optional. Use what they give: demographics (age range, language, tech comfort, accessibility needs), goals and needs, pain points, and traits like patience or risk tolerance should shape which unhappy paths matter and how recovery should read. A hurried first-time user and a cautious admin hit different dead ends at the same step. Never invent persona detail they did not give.)*
4. **"What device or touchpoint will they use it on — web, a native app, a handheld device, a kiosk, or something else? If they're moving, multitasking, or have their hands full while using it, tell me that too."**
   *(Get the actual device and physical context, not just a category label — a handheld scanner used one-handed while walking, a tablet mounted on a moving cart, a large fixed touchscreen at a stationary workstation, and an ordinary desktop app are four different design problems even though some of them all count as "mobile." If a flow spans multiple touchpoints — an admin sets something up on web, a field worker executes it on a handheld scanner — get all of them and which step happens where.)*
5. **"Is this designed for one region today, or does it need to work globally — now or down the line? If you know which regions, name them."**
   *(Doesn't just gate localization on/off — a team that's single-region today but planning to go global should still see localization branches, flagged as forward-looking rather than immediate must-haves, so the flow doesn't need a rebuild later. No expansion plans at all → skip localization entirely. If using pills for this question, use exactly: "Single region," "Global," "Single region, planning to go global," "Not sure." Pair the pills with a free-text field for the named regions, e.g. "Single region: US" or "Global / multi-region: US + India + China". Named regions make localization branches concrete: currency and number formats, date and address formats, languages and scripts, right-to-left layout, local payment methods, data-residency and privacy rules (GDPR, India's DPDP Act, China's PIPL, and so on), and regional outages or restricted services. Use only the regions they name, and with no names, keep the branches generic.)*
6. **"Does this flow depend on any third-party services or integrations — payment processors, carriers, auth providers, and the like?"**
   *(This is exactly where "system/network failure" unhappy paths live — named specifics here beat a generic "the API fails" branch later.)*
7. **"Are there business rules, limits, or compliance requirements that could block or restrict this action?"**
   *(Quotas, regional restrictions, pricing tiers, regulatory constraints — anything that could reject an otherwise valid action.)*
8. **"If this is a redesign — are there existing pain points or issues we already know about?"**
   *(Only bite for existing flows; skip gracefully for net-new ones.)*

If a widget/visualizer tool is available, prefer building a proper elicitation form (real input fields: textareas for the open-ended ones, pills for personas/geographic scope, each paired with a free-text field for persona detail and named regions) over asking piecemeal in chat — it lets people fill in all eight at once instead of a back-and-forth, using the exact question wording above as the field labels. For platform/touchpoint specifically, offer pills for common categories (Web, Native mobile app, Handheld/wearable device, Vehicle/cart-mounted device, Fixed kiosk/large touchscreen, Voice, Other) paired with a free-text field for the specific device and context — the pills alone can't capture "handheld scanner used one-handed while walking" vs. "tablet mounted on a moving cart," and that distinction is exactly the point. If only a simpler button-question tool is available, use it for personas/geographic-scope and ask platform/touchpoint and the rest as open-ended text, verbatim, in the same turn. If neither is available, just ask all eight as a numbered list in one message, using the exact wording above.

Don't block indefinitely on this — if the user answers some and skips others ("just map it, keep it simple"), respect that and proceed with what you have, noting which categories you couldn't tailor as a result (e.g. "I don't know your external dependencies, so the system-failure branches below are generic — tell me what's actually integrated and I'll make them specific").

## Step 1: Establish the flow

If the Step 0 answer for "main actions / steps" gave you a real sequence, use it directly as the backbone rather than re-deriving or second-guessing it — the user telling you the actual steps beats you inferring plausible-sounding ones. Just tighten the wording and check it's at the right level of granularity (see below).

If that answer was vague or skipped, fall back to inferring: propose a reasonable step-by-step happy path yourself from whatever context you have (the problem statement, the flow's name, e.g. "sign up," "checkout," "reset password") and confirm it briefly, rather than stalling on questions. Only ask a clarifying question if the goal itself is ambiguous (e.g., you genuinely can't tell what the user is trying to accomplish).

Use the Step 0 answers here: if there are multiple personas, either map one flow per persona or clearly mark where personas diverge within a single flow (don't silently average them into one generic path).

Keep steps at the level of user actions and system responses, not UI pixels — e.g., "user submits payment form" / "system confirms order," not "user clicks the blue button at coordinates X,Y."

## Step 2: Map the happy path

Write the happy path as a numbered sequence: each step is one user action or one system response, ending at the goal state. This is the backbone everything else attaches to.

## Steps 3-4: Map alternate paths and unhappy paths

**Now load `references/path-categories.md`** — it has the full alternate-path checklist (Step 3), the 17-category unhappy-path checklist split into core/situational (Step 4), and the plain-language translation guide. Follow it in full before moving on.

## Steps 5-6: Produce the output and close the loop

**Now load `references/output-format.md`** — it has the exact doc template, the diagram requirements (all three path types visible directly, never hidden behind a click), and how to wrap up with open questions.
