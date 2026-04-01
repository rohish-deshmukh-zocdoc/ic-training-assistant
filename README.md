<div align="center">

# Incident Commander Training Assistant

### Interactive chatbot for the Zocdoc Incident Commander Training program

[![GitHub Pages](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-blueviolet?style=for-the-badge&logo=github)](https://rohish-deshmukh-zocdoc.github.io/incident-commander-assistant/)
[![Made with Claude](https://img.shields.io/badge/Made%20with-Claude%20Code-purple?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgZmlsbD0id2hpdGUiLz48L3N2Zz4=)](https://github.com/anthropics/claude-code)

<br/>

<table>
<tr>
<td>

```
 _____ _____   _____          _       _
|_   _/ ____| |_   _|        (_)     (_)
  | || |        | |_ __ __ _ _ _ __  _ _ __   __ _
  | || |        | | '__/ _` | | '_ \| | '_ \ / _` |
 _| || |____    | | | | (_| | | | | | | | | | (_| |
|_____\_____|   |_|_|  \__,_|_|_| |_|_|_| |_|\__, |
                                                __/ |
    A S S I S T A N T                          |___/
```

</td>
</tr>
</table>

<br/>

**Your AI-powered guide through Zocdoc's Incident Commander process.**
Ask questions, get step-by-step checklists, and reference the training materials -- all in one place.

[**Launch the Chatbot**](https://rohish-deshmukh-zocdoc.github.io/incident-commander-assistant/) | [**Training Slide Deck**](https://fantastic-adventure-y7yw7y9.pages.github.io/)

</div>

---

## What It Does

The IC Training Assistant is an interactive chatbot that answers questions about the **Zocdoc Incident Commander Training** program. It covers:

| Topic | What You'll Learn |
|-------|-------------------|
| **IC Role & Responsibilities** | What an IC does (and doesn't do), key principles |
| **During an Incident** | Step-by-step checklist from declaration to resolution |
| **Severity & SLAs** | SEV-1/2/3 definitions, mitigation timelines, ack windows |
| **Rootly Tooling** | Slack commands, form buttons, channel features |
| **Emoji Workflows** | Pin, star, memo -- how to build timelines and action items |
| **Escalation** | Who to page, product area mappings, PagerDuty tips |
| **Post-Incident** | Retro deadlines, LSR, retrograde scoring, action item export |
| **Onboarding Checklist** | Everything you need to do before going live on rotation |
| **Interactive Exercises** | Takeaways from real incident scenarios |

---

## Quick Start

### Option 1: Use the Live Page (No Setup Required)

Just open the link in your browser:

> **https://rohish-deshmukh-zocdoc.github.io/incident-commander-assistant/**

---

### Option 2: Install as a Claude Code Skill (CLI Chatbot)

Want to use it directly from your terminal via `/ic-training`? Follow these steps:

#### 1. Clone the repo

```bash
git clone https://github.com/rohish-deshmukh-zocdoc/incident-commander-assistant.git
```

#### 2. Copy the skill files to your Claude Code skills directory

```bash
# Create the skill directory
mkdir -p ~/.claude/skills/ic-training

# Copy the HTML chatbot
cp incident-commander-assistant/index.html ~/.claude/skills/ic-training/ic-chatbot.html
```

#### 3. Download the SKILL.md

Create the file `~/.claude/skills/ic-training/SKILL.md` with the skill definition. You can grab it from this repo's wiki or ask a team member who already has it set up.

> **Tip:** If you're on the IC cohort Slack channel, the SKILL.md has been shared there.

#### 4. Verify it works

Open Claude Code and type:

```
/ic-training
```

This will launch the chatbot in your browser. Or ask a question inline:

```
/ic-training what are the SLAs for SEV-1?
```

---

## How to Use

### In the Browser

1. Open the [live chatbot](https://rohish-deshmukh-zocdoc.github.io/incident-commander-assistant/)
2. Click a **quick action button** or type your question in the chat box
3. Get instant answers with checklists, tables, and links to source materials

**Example questions to try:**
- *"I just got pinged about a Sev2 and I am on call for Incident commander, what do I do now?"*
- *"What's the difference between mitigated and resolved?"*
- *"How do emoji workflows work?"*
- *"What are the SLAs?"*
- *"Who do I page if I don't know the team?"*

### In Claude Code (CLI)

```bash
# Launch the browser chatbot
/ic-training

# Ask inline questions
/ic-training what do I do during an incident?
/ic-training how do I escalate?
/ic-training what is my onboarding checklist?
```

---

## Training Sources

This chatbot is built from the official IC training materials:

| Source | Description |
|--------|------------|
| [Training Slide Deck](https://fantastic-adventure-y7yw7y9.pages.github.io/) | Full slides with screenshots, interactive exercises, and Rootly UI walkthroughs |
| [Session #1 Notes](https://docs.google.com/document/d/1i-sfiPB8GZiyvW7mZDrmxnq3Vw-lupeVj-c250utlVk/edit?tab=t.gvybp59rhjpy) | Mar 17, 2026 -- Getting started, Rootly overview, severity definitions |
| [Session #2 Notes](https://docs.google.com/document/d/1lOUGu4ZamaZLtss-JFIHB-JOs0xnXMy2H7I5NI-g7Pc/edit?tab=t.le3910nsieop) | Mar 24, 2026 -- SLA updates, retrograde scoring, interactive exercises |
| [Session #3 Notes](https://docs.google.com/document/d/1wH7MxN5_ojMkRNeQWC0Ix6QwLTkNWZ2UEdq-FGfA-OM/edit?tab=t.v7pdxdq88tot) | Mar 31, 2026 -- Hands-on Rootly Slack walkthrough, PagerDuty demo |

---

## Making Changes

This site is powered by **GitHub Pages**. To update the chatbot:

```bash
# Clone the repo
git clone https://github.com/rohish-deshmukh-zocdoc/incident-commander-assistant.git
cd incident-commander-assistant

# Edit index.html (the chatbot)
# ... make your changes ...

# Push -- site auto-deploys in ~2 minutes
git add index.html
git commit -m "Update chatbot content"
git push
```

The knowledge base is embedded directly in `index.html` in the `KB` JavaScript object. To add new topics or update answers, edit the corresponding entries there.

---

## Tech Stack

- **Pure HTML/CSS/JS** -- Zero dependencies, no build step
- **GitHub Pages** -- Free hosting, auto-deploy on push
- **Claude Code Skill** -- Optional CLI integration via `/ic-training`

---

<div align="center">

**Built for the Zocdoc IC Cohort** | Training led by **Janice Cheung**

*Generated with [Claude Code](https://github.com/anthropics/claude-code)*

</div>
