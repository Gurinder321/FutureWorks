# CLAUDE.md — Future Works | GTM Client OS

## What This Is

This is the GTM Client OS for **Future Works**. It gives Claude full context to manage this account: who the client is, their ICP, offer, voice, signal strategy, live campaign state, communication history, and decision rationale.

**Managed by:** Gurinder (GTM vendor to Future Works). Template by Harry Rawles.
**Client:** Future Works
**Template version:** see `VERSION` and `CHANGELOG.md`
**Central config:** `company/_config.md`

---

## Quick Reference

| What you want to do | How |
|---------------------|-----|
| Set up this OS for the first time | See `BOOTSTRAP.md` → `Run client onboarder` |
| Use this OS daily | See `OPERATING-RHYTHM.md` |
| Connect MCPs | See `MCP-SETUP.md` |
| Understand acronyms | See `wiki/glossary.md` |

---


## Session Start Protocol (mandatory)

**EVERY Claude session for this client begins by invoking `gtm-skills/pattern-detector.md` FIRST.** No exceptions.

The pattern detector:
1. Reads `company/session-log.md` (last 90 days of invocations)
2. Compares the current user prompt against historical prompts by abstract intent
3. If 3+ matches found AND the pattern is not in "Rejected pattern suggestions" → surfaces a one-line note proposing to forge a new skill via `gtm-skills/skill-forge.md`
4. Writes a session-log entry for the current invocation
5. Hands off to whatever skill should handle the actual user request

This is the auto-improvement mechanism. The OS gets faster and more tailored to your usage patterns with every session.

**Every skill writes its own session-log row.** Pattern-detector runs first and writes the first row, then hands off. Every skill invoked after pattern-detector MUST also write a row at its STEP 0 (per `wiki/_skill-context.md` "Session-Log Write" mandate, enforced by a STEP 0 block in every skill file). Without per-skill rows, the log is sparse and pattern-detection breaks. If a chain invokes 5 sub-skills, the log gets 6 rows (chain + 5 sub-skills).


**What "skip this" means:** reply "skip this" to add the pattern's signature to `Rejected pattern suggestions`. The detector will never re-suggest it.

---
## Behaviour Rules

- Direct, data-led, no fluff. Match the client's voice in `company/voice.md`.
- **Always load `company/MEMORY.md` first** — this is the active scratchpad for current focus, watch-outs, and client preferences.
- Always load context from `wiki/_skill-context.md` before acting.
- PRR is the primary KPI for all copy decisions.
- Never write from memory. Check `company/copy-library.md` first, every time.
- **Spelling:** read `company/voice.md` for client preference. Default UK English if voice.md unspecified.
- No unnecessary hedging. Short sentences. Active voice.
- Numbers as digits (5 not five).
- Never use: "leverage", "synergy", "game-changer", "revolutionary", "cutting-edge", "hope this helps".

---

## Safety Guard

### Blocked without explicit approval:
1. Sending any external comms on behalf of the client
2. Making changes to the client's Instantly workspace (pausing, deleting, editing campaigns)
3. Sharing campaign data or client information externally
4. Any financial operations (billing, refunds, invoices)
5. Auto-handling hostile replies, GDPR-flagged messages, or legal threats — always escalate

**When blocked:** state exactly what you were about to do, ask for explicit approval, wait before retrying.

---

## Skill Routing Table

### Setup and operating rhythm

| User intent | Skill | When |
|-------------|-------|------|
| (automatic: every session) | gtm-skills/pattern-detector.md | **Runs FIRST every session.** Logs invocations to session-log |
| "Onboard new client" / "Set up the OS" | gtm-skills/client-onboarder.md | First time on a fresh clone |
| "Run weekly review" / "Friday review" | gtm-skills/weekly-reviewer.md | Weekly review loop |
| "Run pre-launch check" | gtm-skills/pre-launch-check.md | Before any campaign goes live |

### Copy and campaigns

| User intent | Skill | When |
|-------------|-------|------|
| "Write a cold email sequence" | gtm-skills/cold-email-writer.md | New campaign or rewrite |
| "Launch the campaign" | gtm-skills/campaign-launcher.md | Pre-flight before going live |
| "Diagnose campaign" / "Why is PRR low" | gtm-skills/campaign-optimiser.md | Performance issue |
| "Analyse campaign data" | gtm-skills/campaign-analyst.md | Performance review |

### Strategy and sourcing

| User intent | Skill | When |
|-------------|-------|------|
| "Personalise at scale" | gtm-skills/personalization-strategist.md | High-tier prospect campaigns |
| "Build / qualify lead list" | gtm-skills/list-builder.md | New list or list quality issue |

### Operations and crises

| User intent | Skill | When |
|-------------|-------|------|
| "Handle this reply" | gtm-skills/reply-handler.md | Any inbound reply |
| "Handle client request" | gtm-skills/client-request-handler.md | Mid-week client ask |
| "Diagnose deliverability" | gtm-skills/deliverability-doctor.md | Bounces, spam, blacklists |
| "Incident" / "Domain blacklisted" / "Bounce spike" | gtm-skills/incident-responder.md | Critical/high severity issue |

### Helper skills (invoked by other skills, not by user)

| Skill | Invoked by |
|-------|-----------|
| gtm-skills/fresh-eyes-reviewer.md | Pass 2 review for cold-email-writer |

---

## File Structure

```
client-os/
├── README.md              # Human-facing intro
├── BOOTSTRAP.md           # Setup entry point
├── OPERATING-RHYTHM.md    # Daily/weekly/monthly/quarterly cadence
├── MCP-SETUP.md           # MCP connection guide
├── CHANGELOG.md           # Template version history
├── VERSION                # Semver
├── LICENSE                # Usage rights
├── .gitignore             # Committed file hygiene
├── CLAUDE.md              # This file — hub for Claude
├── INDEX.md               # Content catalog
│
├── company/               # Per-client context (this client only)
│   ├── _config.md         # Central config — referenced by other files
│   ├── overview.md        # Identity, SLA, success criteria
│   ├── icp.md             # Target profile, signals
│   ├── offer.md           # What they sell
│   ├── voice.md           # Tone, banned words, spelling
│   ├── campaign-state.md  # Live campaigns, infrastructure, tools
│   ├── decision-log.md    # Why decisions were made
│   ├── competitive-intel.md
│   ├── comms-log.md       # Client communications
│   ├── copy-library.md    # Top performers + graveyard
│   ├── test-log.md        # Split test history
│   ├── MEMORY.md          # Always-loaded scratchpad: focus, watch-outs
│   └── session-log.md     # Per-invocation log (powers pattern-detector)
│
├── wiki/                  # Shared knowledge — same across all clients
│   ├── _skill-context.md  # Standard skill preamble (every skill loads this)
│   ├── copywriting-101.md # Canonical rules + 4-part formula + sequence
│   ├── copywriting-frameworks.md
│   ├── offer-framework.md
│   ├── scientific-method.md
│   ├── signal-sourcing.md
│   ├── buying-triggers.md
│   ├── personalization-at-scale.md
│   ├── deliverability.md
│   ├── list-building.md
│   ├── atl-btl-messaging.md
│   ├── subject-lines.md
│   ├── psychological-principles.md
│   ├── objection-library.md
│   ├── industry-vernacular.md
│   ├── email-benchmarks.md
│   ├── glossary.md
│   └── diagrams.md
│
├── gtm-skills/            # AI skill definitions (frontmatter + content)
│   ├── pattern-detector.md         # RUNS FIRST EVERY SESSION — auto-improvement loop
│   ├── client-onboarder.md         # RUN FIRST on a fresh clone
│   ├── weekly-reviewer.md          # RUN EVERY FRIDAY — compounding loop
│   ├── pre-launch-check.md         # Gate for placeholder validation
│   ├── cold-email-writer.md
│   ├── campaign-launcher.md
│   ├── campaign-optimiser.md
│   ├── reply-handler.md
│   ├── client-request-handler.md
│   ├── incident-responder.md
│   ├── personalization-strategist.md
│   ├── list-builder.md
│   ├── deliverability-doctor.md
│   ├── campaign-analyst.md
│   └── fresh-eyes-reviewer.md      # Helper sub-agent (invoked by other skills)
│
├── examples/              # Reference examples
│   ├── sample-weekly-review.md    # What a Friday review looks like
│   ├── sample-client-report.md    # What a weekly report looks like
│   └── sample-decision-log-entries.md
│
├── tests/                 # OS regression tests
│   ├── README.md
│   ├── test-onboarding.md
│   └── test-cold-email-writer.md
│
├── raw/                   # Pre-call worksheets, call notes
│   └── onboarding-intake.md       # Pre-call client worksheet
│
├── assets/                # Index of external assets (case studies, decks)
│   └── README.md
│
└── .github/
    └── ISSUE_TEMPLATE/    # Issue templates for tracking
        ├── client-request.md
        ├── campaign-launch.md
        ├── incident.md
        └── optimization-test.md
```

---

## Credentials

All API keys in 1Password. Never commit credentials.

See `MCP-SETUP.md` for connection details.

---

## Source Knowledge

This OS combines:
- **Primary methodology** — copywriting principles, scientific method, offer framework (curated by Harry)
- **ColdIQ GTM Skills** — signal sourcing, personalisation at scale, ATL/BTL, deliverability, frameworks library

Primary methodology is the source of truth. ColdIQ material extends it.
