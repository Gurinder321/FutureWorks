# Campaign State — {{CLIENT_NAME}}

Live status of all outbound campaigns. Update this file when campaigns launch, pause, change, or are retired.

**Last updated:** {{DATE}}

---

## Active Campaigns

| Campaign name | Signal | Launch date | Mailboxes | Sends/day | Status | Health |
|--------------|--------|-------------|-----------|-----------|--------|--------|
| {{Name}} | {{Signal type}} | {{Date}} | {{n}} | {{n}} | Active | Green / Amber / Red |

---

## Tools & Tech Stack (W4)

Tracks what tooling is configured for this client. Affects which signals can be detected and which workflows can run.

| Tool | Connected | Notes |
|------|-----------|-------|
| Instantly | {{Yes/No}} | Primary sender |
| Clay | {{Yes/No}} | If used for enrichment |
| RB2B | {{Yes/No}} | Website visitor detection |
| LoneScale / Champify | {{Yes/No}} | Champion job change detection |
| Findymail | {{Yes/No}} | Email verification |
| Apollo | {{Yes/No}} | Lead database |
| HeyReach | {{Yes/No}} | LinkedIn (if multichannel) |
| Slack | {{Yes/No}} | Reply alerts |
| Notion | {{Yes/No}} | Client comms / context |

---

## Campaign Detail

### {{Campaign Name 1}}

**Signal:** {{What trigger this campaign targets}}
**ICP slice:** {{Which subset of ICP this campaign targets}}
**Sequence:** {{n}}-step email

| Step | Day | Subject line | Purpose |
|------|-----|-------------|---------|
| Email 1 | Day 0 | {{Subject}} | Main pitch |
| Email 2 | Day 3 | {{Subject}} | Follow-up, different angle |
| Email 3 | Day 7 | {{Subject}} | Final touch |

**Current metrics (last 30 days):**
- Sends: {{n}}
- Reply rate: {{%}}
- PRR: {{%}}
- Meetings booked: {{n}}
- Bounce rate: {{%}}

**Health:** Green / Amber / Red
**Notes:** {{Any issues, things to watch, or context}}

---

## Infrastructure

**Seeded 2026-10-29 from Gurinder.** Phase 1 sends use Future Works's own mailboxes. Gurinder's mailboxes are still warming and take over after.

| Set | Provider | Mailboxes | Per domain | Warm status |
|-----|----------|-----------|-----------|-------------|
| Future Works (client) | Google | **58 listed** (client said 50) | 14 domains, 2-5 each (not a flat 4) | Warmed for months, ready to send |
| Gurinder (agency) | Google `{{TO CONFIRM}}` | 100 | 2 (~50 domains) | Warming, ~7 days left (as of 2026-10-29) |

**Target:** 5 held meetings per week. Plan for 3,000-5,000 sends per week (about 12-20 per mailbox per day on the 50 warmed mailboxes).

**Client inbox list:** `raw/fw-sending-inboxes.txt` (58 addresses, 14 domains: 5x nowfutureworks.xyz, getfutureworks.company, getfutureworks.click, futureworks.one, explorefutureworks.xyz; 4x thefutureworks.xyz, myfutureworks.xyz, joinfutureworks.xyz, joinfutureworks.click, gofutureworks.xyz, getfutureworks.one, atfutureworks.xyz; 3x tryfutureworks.one; 2x futureworksemail.com). Sender names: chris (14), matt.l (14), matt (13), michael (11), michael.wadden (6). These are the client's mailboxes, used for about 1 week until Gurinder's 100 are warm.

**Open:** which of the 58 are actually warm, their sender-name personas, and tracking domain setup, Instantly workspace URL and ID, MCP connection.

| Resource | Detail | Status |
|----------|--------|--------|
| Sending domains | {{List domains}} | Active / Warming |
| Mailboxes | {{n}} mailboxes across {{n}} domains | Active |
| Warmup status | {{All warmed / some warming}} | — |
| Instantly workspace | {{Workspace name / URL}} | Connected |
| LinkedIn accounts | {{n accounts}} | {{Status}} |

---

## Paused / Completed Campaigns

| Campaign name | Reason | Paused date | Notes |
|--------------|--------|-------------|-------|
| {{Name}} | {{Why paused}} | {{Date}} | {{What to do if reactivating}} |

---

## Benchmarks for This Client

| Metric | Target | Acceptable | Needs attention |
|--------|--------|-----------|-----------------|
| PRR | 1.5%+ | 0.5-1.5% | Under 0.5% |
| Reply rate | 3%+ | 1-3% | Under 1% |
| Bounce rate | Under 2% | 2-4% | Over 4% |
| LinkedIn acceptance | 35%+ | 20-35% | Under 20% |

---

## State Notes

{{Anything about the current state that does not fit the tables above — deliverability concerns, list quality issues, signals performing differently than expected, etc.}}