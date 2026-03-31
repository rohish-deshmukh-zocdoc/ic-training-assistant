---
name: ic-training
description: Incident Commander training chatbot - answers questions about IC role, responsibilities, Rootly tooling, escalation, SLAs, and guides you through next steps with references to the training materials
argument-hint: <your question about IC training>
---

# ic-training -- Incident Commander Training Assistant

## Purpose

Interactive chatbot that answers questions about the Zocdoc Incident Commander Training program. It uses the official training materials as the source of truth and can guide you through processes, next steps, and actions.

## Sources of Truth

1. **IC Training Repo (primary):** https://github.com/Zocdoc/incident-command-training/ (15 markdown files covering all IC topics)
2. **Training Slide Deck (GitHub Pages):** https://fantastic-adventure-y7yw7y9.pages.github.io/
3. **Session #1 Notes (Mar 17, 2026):** https://docs.google.com/document/d/1i-sfiPB8GZiyvW7mZDrmxnq3Vw-lupeVj-c250utlVk/edit?tab=t.gvybp59rhjpy
4. **Session #2 Notes (Mar 24, 2026):** https://docs.google.com/document/d/1lOUGu4ZamaZLtss-JFIHB-JOs0xnXMy2H7I5NI-g7Pc/edit?tab=t.le3910nsieop
5. **Session #3 Notes (Mar 31, 2026):** https://docs.google.com/document/d/1wH7MxN5_ojMkRNeQWC0Ix6QwLTkNWZ2UEdq-FGfA-OM/edit?tab=t.v7pdxdq88tot

When the user asks a question, **first check the embedded knowledge base below**. If additional detail is needed or the user asks about something not covered, use Glean `read_document` (via a subagent) to fetch the latest content from the Google Docs above, or direct the user to the training slide deck URL.

## Invocation

- `/ic-training` -- launch the IC Training chatbot HTML page in a browser
- `/ic-training chat` -- launch the chatbot HTML page
- `/ic-training <any question>` -- answer inline in the terminal

When invoked without a specific question (or with `chat`), **always launch the HTML chatbot page** by running:
```
open /Users/rohish.deshmukh/.claude/skills/ic-training/ic-chatbot.html
```

When invoked with a specific question, answer inline from the knowledge base below AND mention they can run `/ic-training` to open the full interactive chatbot.

## How to Respond

1. **Answer from the knowledge base first.** Use the embedded training content below.
2. **Be action-oriented.** When the user asks "what do I do now" or similar, give them a clear checklist of next steps based on their role and the training status.
3. **Reference sources.** Point the user to the relevant training URL or section for deeper reading.
4. **Use the slide deck for visuals.** When the user needs to see images, screenshots, or interactive exercises, direct them to the training slide deck: https://fantastic-adventure-y7yw7y9.pages.github.io/
5. **Keep it concise but complete.** Provide enough detail to act on, but don't overwhelm.
6. **If the user asks about Rootly UI, Slack commands, or emoji workflows**, refer them to Session #3 and the training slide deck for screenshots and hands-on walkthroughs.

---

## KNOWLEDGE BASE

### Overview

The IC Training program establishes a cohort of 8 Incident Commanders for 24/7 SEV-1 coverage at Zocdoc. Previously, Brandie Burditt was the sole IC. The first cohort was selected based on senior director recommendations.

**Cohort #1 Members:** Hank Bao, Noah Rowland, Mukesh Chhatani, Noah Weinthal, Brandie Burditt, Janice Cheung, Rohish Deshmukh, Elizabeth Ford, James Collins, Chris Smith, John Penner, Mustafa Rizvi

**Training Sessions Completed:**
- Session #1 (Mar 17, 2026) -- Getting started, Rootly overview, severity definitions, communication etiquette, incident lifecycle
- Session #2 (Mar 24, 2026) -- SLA updates, retrograde scoring, interactive exercises (Login Failure, FC Deploy, Total Outage)
- Session #3 (Mar 31, 2026) -- Hands-on Rootly Slack walkthrough, PagerDuty escalation demo, form buttons, emoji workflows, action item export

---

### The IC Role

- **What:** Single decision-maker during an active SEV-1 incident
- **Focus:** Coordination, communication, delegation -- NOT debugging or fixing code
- **Goals:** Facilitate quickest path to mitigation and resolution; pull in any team; page any responders
- **Scope:** Exclusively SEV-1 incidents for this cohort
- **Key principle:** "Drive the process, don't debug"

---

### Schedule & Rotation

- **Cadence:** 7-day weekly shift, Monday to Monday, 9:00 AM to 9:00 AM
- **Coverage:** 24/7 for all SEV-1 incidents
- **Roles:** Primary IC and Secondary IC
- **PTO/Conflicts:** IC is responsible for scheduling PagerDuty overrides and coordinating swaps with secondary
- **If on-call AND IC simultaneously:** Coordinate with someone to swap one of the roles, or delegate IC to secondary
- **Onboarding:** Training -> Shadow -> Reverse Shadow -> Official rotation
- **First shifts:** Noah Rowland (first week, shadow), Noah Weinthal (second week, reverse shadow), then others rotate

---

### Severity Definitions

| Severity | Definition | SLA (Mitigation) | Ack SLA | Resolution SLA | Exec Summary Cadence |
|----------|-----------|-------------------|---------|----------------|---------------------|
| **SEV-1 (Critical)** | Customer-facing workflows CANNOT be completed | 1 hour | 15 min | 1 hour | Every 30 minutes |
| **SEV-2 (Major)** | Degraded or noticeably impacted state | 4 hours | 15 min | -- | Every 60 minutes |
| **SEV-3 (Minor)** | Would any customers notice today? No. | Best effort | -- | -- | -- |

- **"Customer"** includes patients, providers, stakeholders, engineering, finance, product analysts, API consumers, branded directory partners
- **Always round UP** if severity is ambiguous -- better to be called more often
- **Downgrade rule:** If downgraded (e.g. SEV-2 to SEV-3), absolved from original SLA
- SLA clock does NOT stop while you sleep -- 4-hour SEV-2 SLA applies even at 2 AM

**Examples:**
- SEV-1: Booking is down, KMS throttled with multiple service failures
- SEV-2: Degraded auth0 API responses, search service directory crash
- SEV-3: DLQ key redrives, deploy rollbacks with no customer impact

---

### Rootly Platform & Tooling

**Creating an Incident:**
- Slack command: `/incident new`
- Auto-generates: Jira outage ticket, PagerDuty alert, email notification, Slack announcements, Confluence retrospective (SEV-1 & SEV-2)
- Can also be created via Jira outage ticket (new Q2 feature for QA/CS teams)
- Check existing incidents: `/incident list` or check #prod channel or Rootly dashboard

**Incident Channel Features:**
- **Channel bookmarks:** Google Meet, Rootly, status page, TeamCity rollback guide
- **Quick links:** Rollback guide, service ownership/escalation policies, vendor contact list, team DBR/SRE Slack handles
- **Form buttons (pinned at top):** Escalate, Assign Roles, Update, Run Workflow

**Key Form Buttons:**
1. **Escalate** -- Page in responders via PagerDuty escalation policy or specific users (can override on-call rotation)
2. **Assign Roles** -- Self-assign as IC, delegate Technical Lead, Scribe, Communications Lead, Retro Lead
3. **Update** -- Change severity, executive summary, detection time
4. **Run Workflow** -- Create/regenerate Confluence retrospective, send comms to #prod

---

### Emoji Workflows

| Emoji | Action | Result |
|-------|--------|--------|
| **Pin** | Pin a message | Adds to incident timeline (auto-captured in Confluence retrospective) |
| **Star** | Star a message | Marks as action item (exportable to Jira) |
| **Memo** | Memo emoji | Marks as action item (exportable to Jira) |

- Pinned messages get a green checkmark confirmation
- Eyes and flame emojis do NOT get checkmarks
- Action items (star/memo) can be exported to Jira tickets via the action items modal -- select project key and issue type

---

### Steps During an Incident (Checklist)

1. **Declare yourself as IC** -- Announce in the incident Slack channel; use "Assign Roles" to self-assign
2. **Escalate to service owners** -- Use the "Escalate" form button or product areas mapping; escalate BEFORE diagnosis
3. **Investigate & assess severity** -- Assess blast radius, identify exit criteria, quantify impact (bookings, revenue, reputation)
4. **Mitigate the incident** -- Rollback, feature flag, failover, or hotfix; mitigated != resolved (temporary state, root cause not fixed)
5. **Resolve the incident** -- Verify exit criteria, update executive summary, confirm stable for 15+ minutes
6. **Create action items** -- Pin messages with star/memo emoji, export to Jira tickets
7. **Assign retrospective lead** -- Delegate the retro owner for post-incident process

**Communication Standards:**
- All communication in the dedicated Slack incident channel (no side conversations)
- Threaded comments for specific investigations
- Google Meet conversations must be transcribed to Slack
- If radio silence for 30 min, push for updates
- Screenshots of dashboards at key moments for timeline context

**Boilerplate IC Announcement:**
> "I'm taking over as Incident Commander. Here's what we're seeing: [impact summary]. We need [SMEs/teams]. Current status: [investigating/mitigating]. Next update in 30 minutes."

---

### After an Incident

**Post-Resolution Checklist:**
1. Assign retrospective lead (retro owner)
2. Mark action items with emojis (star/memo)
3. Export action items to Jira
4. Verify required fields populated (root cause, resolution, timestamps, detection time)
5. Update executive summary

**SLA Deadlines:**
- 5 business days: Retro document completion
- 1 week: Retro meeting held
- 2 weeks: LSR (Live Site Review) presentation
- 14 days total: Declared to Done state

**Retrograde Scoring:**
- Incidents are scored based on data completeness in Rootly
- Points for: documented root cause, MTTM/MTTR SLA adherence, action items created, automated vs manual detection
- Automated alert detection = more points; manual detection = fewer points
- Grades and SLA breach reports are published to leadership
- Recurring patterns (same root cause) are flagged

---

### Incident Lifecycle States

`Declared` -> `Triage` -> `Active` -> `Mitigated` -> `Resolved` -> `Pending Retro` -> `Pending LSR` -> `Pending Action Items` -> `Done`

- Mitigated = blast radius reduced, root cause NOT fixed
- Resolved = root cause addressed, no recurrence expected, stable 15+ min
- Jira outage ticket moves through these same states
- Violations to state progression are reported to leadership

---

### IC Handoff & Long-Running Incidents

- Use explicit handoff communication in the Slack channel
- Secondary IC can take over if primary is fatigued or has been on for extended periods
- "I need to step back" is valid -- communicate clearly and ensure handoff is documented
- IC health and well-being is a priority

---

### Escalation Reference

**Product Areas Mapping (Coming Q2):**
- New dropdown in "create incident" modal maps product areas (from Miro board sticky notes) to PagerDuty escalation policies
- Type 3+ keystrokes to autocomplete and find the right team
- Zero guesswork -- correct service owner paged instantly
- Source: Miro board export -> spreadsheet -> Rootly workflows (eventually ROI automated sync)

**If you don't know who to page:**
- Message a director or VP to recommend the right responders
- Use the vendor contacts quick link in the incident channel
- @ mention team-dbre or team-sre Slack handles

---

### Interactive Exercise Takeaways

**Exercise 1: SEV-1 Login Failure (Mar 2, 2026)**
- First step: Declare IC, NOT troubleshoot
- If it impacts the business, declare it
- After rollback, monitor for lagging indicators before escalating further
- Over-communicate; never watch in silence
- Action: Ask product analytics to verify if metrics are normal or anomalous

**Exercise 2: FC Package Deploy (Friday 3:30 PM)**
- Don't deploy at 3:30 PM on Friday with 2 weeks of bundled changes
- Platform-specific alerts are critical (mobile web was missed)
- Need top-level cross-org dashboards for key metrics
- Caught by luck (VP saw report Saturday morning), not by structure
- Action items: synthetics for mobile web, anomaly detection by platform, deploy freeze/mandatory monitoring after 2 PM Fridays

**Exercise 3: 16-Minute Total Outage (SCP Removal)**
- Every team paged at once -> centralize, look for shared upstream root cause
- SCPs are high-risk infrastructure changes requiring strict change management
- Need formal risk assessment alongside change management
- Change request tickets with approval gates for core infrastructure

---

### Key Slack Commands

| Command | Purpose |
|---------|---------|
| `/incident new` | Create a new incident |
| `/incident list` | List active incidents |

---

### Session #3 Hands-On Highlights (Rootly Slack Experience)

- **Escalate button:** Opens "Add Responders" modal; select escalation policy OR specific users; overrides on-call rotation
- **Assign Roles:** Self-assign IC, delegate Technical Lead, Scribe, Communications Lead
- **Action Items modal:** Pre-populated guidance for ICs; pin messages to capture timeline
- **Run Workflow:** Create/regenerate Confluence retro, send #prod announcements
- **Update button:** Adjust severity, exec summary, detection time as new info emerges
- **Mitigate vs Resolve:** Mitigate = temporary (reduce blast radius); Resolve = root cause fixed
- **Jira export:** Action items -> select project key -> auto-creates Jira tickets AND appears in Confluence retro
- **Coming soon:** Auto-escalation based on product area mappings (no manual escalation needed)
- **Documentation improvement:** Moving to checklist format for high-stress incident use

For screenshots and hands-on walkthroughs of all these features, visit the training slide deck:
**https://fantastic-adventure-y7yw7y9.pages.github.io/**

---

### What Should I Do Now? (Onboarding Checklist)

If you're a new IC cohort member, here's your action plan:

- [ ] **Review the training slide deck** -- https://fantastic-adventure-y7yw7y9.pages.github.io/ (includes all slides, interactive exercises, and screenshots)
- [ ] **Read Session #1 notes** -- [Session #1 Doc](https://docs.google.com/document/d/1i-sfiPB8GZiyvW7mZDrmxnq3Vw-lupeVj-c250utlVk/edit?tab=t.gvybp59rhjpy)
- [ ] **Read Session #2 notes** -- [Session #2 Doc](https://docs.google.com/document/d/1lOUGu4ZamaZLtss-JFIHB-JOs0xnXMy2H7I5NI-g7Pc/edit?tab=t.le3910nsieop)
- [ ] **Read Session #3 notes** -- [Session #3 Doc](https://docs.google.com/document/d/1wH7MxN5_ojMkRNeQWC0Ix6QwLTkNWZ2UEdq-FGfA-OM/edit?tab=t.v7pdxdq88tot)
- [ ] **Confirm your PagerDuty seat** -- Ensure you have a Rootly seat and PagerDuty access
- [ ] **Try `/incident new` in Slack** -- Familiarize yourself with the incident creation modal (use test channel)
- [ ] **Practice the interactive exercises** -- Go through the tabletop exercises in the slide deck
- [ ] **Shadow an IC shift** -- Observe how Noah Rowland or Noah Weinthal handle a SEV-1
- [ ] **Reverse shadow** -- Take the lead with a senior IC observing you
- [ ] **Go live** -- Join the weekly rotation once you're comfortable
- [ ] **Keep Miro board updated** -- Ensure your team's product areas and escalation mappings are current
- [ ] **Make your team go through Rootly exercise** -- Per John Penner's action item, mandate team training on Rootly and runbook playbooks

---

### FAQ

**Q: Do I need to be a technical expert?**
A: No. The IC role is about coordination, communication, and delegation. You don't debug or fix code.

**Q: What if I'm already on-call for my team and a SEV-1 hits?**
A: Coordinate with someone to swap one role, or delegate IC to the secondary.

**Q: What if I'm too tired during a long incident?**
A: Say "I need to step back" in the Slack channel, hand off to secondary, and document the handoff clearly.

**Q: Can I downgrade a severity?**
A: Yes, but you must communicate the reason with data/justification in the Slack channel.

**Q: What if I page the wrong person?**
A: Apologize and page the correct person. It's better to over-escalate than under-escalate.

**Q: Where can I see all the screenshots and Rootly UI?**
A: Visit the training slide deck at https://fantastic-adventure-y7yw7y9.pages.github.io/

**Q: Who do I contact for more training?**
A: Email Noah Rowland or reach out to Janice Cheung.
