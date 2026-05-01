# User Manual

**Version**: 1.0.0
**Last Updated**: 2025-01-01

---

## Table of Contents

1. [Getting Started](#1-getting-started)
2. [Daily Usage](#2-daily-usage)
3. [Content Creation Workflows](#3-content-creation-workflows)
4. [Working with Skills](#4-working-with-skills)
5. [Managing Your Knowledge Base](#5-managing-your-knowledge-base)
6. [Tips and Tricks](#6-tips-and-tricks)
7. [Common Tasks Reference](#7-common-tasks-reference)

---

## 1. Getting Started

### 1.1 Prerequisites

Before you begin, ensure you have:

- [ ] Cursor editor installed (https://cursor.sh)
- [ ] Claude Code extension installed
- [ ] Claude subscription OR Anthropic API key
- [ ] The `my-writing-system` folder on your computer

### 1.2 First-Time Setup (30-60 minutes)

#### Step 1: Open the Project
```
1. Launch Cursor
2. File → Open Folder
3. Navigate to my-writing-system
4. Click "Open"
```

#### Step 2: Verify Claude Code
```
1. Look for Claude Code panel (usually right side or bottom)
2. If not visible: View → Command Palette → "Claude Code: Open"
3. Type "What skills are available?" to test connection
```

#### Step 3: Create Your Voice DNA
```
1. In Claude Code, type: "Help me create my voice DNA profile"
2. When prompted, provide 3-10 writing samples
3. Answer questions about your style
4. Review the generated profile
5. Confirm to save to /context/voice-dna.json
```

#### Step 4: Create Your ICP
```
1. Type: "Help me create my ICP"
2. Answer interview questions about your audience
3. Be specific - "founders" is too broad, "SaaS founders with 10-50 employees" is better
4. Confirm to save to /context/icp.json
```

#### Step 5: Create Your Business Profile
```
1. Type: "Help me create my business profile"
2. Answer questions about your business
3. Include current offerings and pricing
4. Confirm to save to /context/business-profile.json
```

### 1.3 Verification

Test your setup:
```
"Write a short LinkedIn post about [any topic you cover]"
```

The output should:
- ✓ Match your voice (not generic AI)
- ✓ Address your audience's perspective
- ✓ Include appropriate CTA

---

## 2. Daily Usage

### 2.1 Starting a Session

```
1. Open Cursor
2. Open my-writing-system folder (if not already open)
3. Open Claude Code panel
4. Start creating content
```

Claude automatically loads `claude.md` at startup—no action needed.

### 2.2 Basic Commands

#### Creating Content
```
"Write a LinkedIn post about [topic]"
"Create a Twitter thread on [topic]"
"Write 5 Substack notes from this newsletter"
"Help me write a thought leadership piece on [topic]"
```

#### Getting Help
```
"What skills are available?"
"How should I structure a LinkedIn post?"
"What frameworks do you have for Twitter threads?"
```

#### Working with Files
```
"Read my latest newsletter draft"
"Save this to my drafts folder"
"Create a new file for these notes"
```

### 2.3 Conversation Patterns

#### Good Request Pattern
```
User: "Write a LinkedIn post about why AI writing systems beat prompts"
Claude: [Reads context profiles, invokes linkedin-post skill, generates post]
User: "Make it more conversational"
Claude: [Adjusts based on voice DNA]
User: "Perfect, save it to drafts"
Claude: [Saves to /knowledge/drafts/]
```

#### Batch Request Pattern
```
User: "Write 10 Substack notes from my latest newsletter in /knowledge/drafts/newsletter-jan.md"
Claude: [Reads newsletter, invokes substack-note skill, generates 10 notes]
User: "These are great. Save them to a new file"
Claude: [Creates file in knowledge folder]
```

### 2.4 Session Management

#### Starting Fresh
Each new Claude Code session starts clean. To continue previous context:
```
"Read my latest draft in /knowledge/drafts/ and continue working on it"
```

#### Multiple Chats
You can open multiple Claude Code panels:
```
1. Click "+" in Claude Code panel
2. Each panel is a separate conversation
3. Useful for working on different content simultaneously
```

---

## 3. Content Creation Workflows

### 3.1 LinkedIn Post Workflow

```
Step 1: Request
─────────────────
"Write a LinkedIn post about [topic]"

Step 2: Claude Process (automatic)
─────────────────
→ Reads voice-dna.json
→ Reads icp.json
→ Invokes linkedin-post skill
→ Applies appropriate framework

Step 3: Review Output
─────────────────
- Check hook strength
- Verify voice match
- Confirm CTA is appropriate

Step 4: Iterate (if needed)
─────────────────
"Make the hook more punchy"
"Add a personal story element"
"Change the CTA to newsletter signup"

Step 5: Finalize
─────────────────
"Save this to drafts" OR copy to LinkedIn
```

### 3.2 Twitter Thread Workflow

```
Step 1: Request
─────────────────
"Create a Twitter thread about [topic]"
OR
"Turn this article into a Twitter thread"

Step 2: Review Structure
─────────────────
- Hook tweet (should work standalone)
- Body tweets (one idea each)
- CTA tweet

Step 3: Iterate
─────────────────
"Make tweet 3 shorter"
"Add more specific examples"
"Change the hook to be more contrarian"

Step 4: Format Check
─────────────────
Each tweet should be under 280 characters
(Claude tracks this automatically)
```

### 3.3 Newsletter Repurposing Workflow

```
Step 1: Add Newsletter to Knowledge
─────────────────
Save newsletter to /knowledge/drafts/newsletter-name.md

Step 2: Request Batch Content
─────────────────
"Read the newsletter at /knowledge/drafts/newsletter-name.md and create:
- 10 Substack notes
- 3 LinkedIn posts
- 1 Twitter thread"

Step 3: Review and Organize
─────────────────
"Save the Substack notes to /knowledge/drafts/notes-jan.md"
"Save the LinkedIn posts to /knowledge/drafts/linkedin-jan.md"

Step 4: Schedule
─────────────────
Copy content to scheduling tool (Buffer, Hootsuite, etc.)
```

### 3.4 Thought Leadership Workflow

```
Step 1: Brainstorm
─────────────────
"I want to write about [broad topic].
What angles would resonate with my ICP?"

Step 2: Choose Angle
─────────────────
"Let's go with angle #2 - the contrarian take"

Step 3: Generate Outline
─────────────────
"Create an outline for this thought leadership piece"

Step 4: Write Sections
─────────────────
"Write the introduction"
"Write section 1"
[Continue through sections]

Step 5: Review and Polish
─────────────────
"Review the full piece for voice consistency"
"Strengthen the conclusion"
```

### 3.5 Email Sequence Workflow

```
Step 1: Define Parameters
─────────────────
"I need a welcome email sequence for new subscribers.
- 5 emails
- Goal: introduce my content and sell my course
- Timeline: over 2 weeks"

Step 2: Generate Sequence
─────────────────
Claude generates all 5 emails with:
- Subject lines
- Preview text
- Body content
- CTAs
- Timing recommendations

Step 3: Review Each Email
─────────────────
"Make email 2 more personal"
"Add social proof to email 4"

Step 4: Export
─────────────────
Copy to email platform (ConvertKit, Mailchimp, etc.)
```

---

## 4. Working with Skills

### 4.1 Understanding Skill Invocation

Skills are **automatically invoked** based on your request:

| You Say | Skill Used |
|---------|------------|
| "Write a LinkedIn post" | linkedin-post |
| "Create a Twitter thread" | twitter-thread |
| "Help me with my LinkedIn profile" | linkedin-profile-optimizer |
| "Write Substack notes" | substack-note |
| "Create an email sequence" | sales-email-sequence |
| "Write a how-to guide" | how-to-guide |

### 4.2 Checking Available Skills

```
"What skills are available?"
"List all writing skills"
"What can you help me create?"
```

### 4.3 Using Specific Frameworks

Each skill has multiple frameworks. Request specific ones:

```
# LinkedIn
"Use the contrarian framework for this LinkedIn post"
"Write this as a list post"

# Twitter
"Use the story thread framework"
"Make it a how-to thread"

# Email
"Create a launch sequence"
"Make it a re-engagement sequence"
```

### 4.4 Skill Discovery Tips

- Skills are described in `claude.md` under Skills Guide
- Each skill folder has `SKILL.md` with full documentation
- Ask Claude "How does the [skill-name] skill work?"

---

## 5. Managing Your Knowledge Base

### 5.1 Knowledge Folder Structure

```
knowledge/
├── drafts/     # Work in progress
├── notes/      # Ideas, research, outlines
└── archive/    # Published content
```

### 5.2 Adding Content

#### Save from Claude
```
"Save this to /knowledge/drafts/filename.md"
```

#### Manual Addition
1. Create file in appropriate folder
2. Use descriptive filename: `2025-01-15_topic_type.md`

### 5.3 Organizing for Scale

As content grows, create subfolders:

```
knowledge/
├── drafts/
│   ├── linkedin/
│   ├── twitter/
│   └── newsletters/
├── notes/
│   ├── ideas/
│   ├── research/
│   └── outlines/
└── archive/
    ├── 2024/
    └── 2025/
```

### 5.4 Using Knowledge for Repurposing

```
# Point to specific file
"Repurpose /knowledge/archive/2025/newsletter-jan.md into 10 LinkedIn posts"

# Search knowledge
"Find my content about AI writing and create a thread from it"
```

### 5.5 Knowledge Base Best Practices

| Do | Don't |
|----|-------|
| Use consistent naming | Random filenames |
| Archive published content | Delete after publishing |
| Organize by type or date | Dump everything in one folder |
| Keep originals | Overwrite with edits |

---

## 6. Tips and Tricks

### 6.1 Getting Better Output

#### Be Specific
```
# Less effective
"Write a post"

# More effective
"Write a LinkedIn post about how to set up AI writing systems,
targeting SaaS founders, with a hook about saving time"
```

#### Provide Context
```
"Based on my latest newsletter about AI tools,
write 5 LinkedIn posts that cover the key points"
```

#### Iterate Deliberately
```
"Make it punchier"
"Add a personal anecdote"
"Make the CTA more specific"
```

### 6.2 Batch Content Creation

```
# Create multiple at once
"Write 10 Substack notes, each exploring a different aspect of [topic]"

# Repurpose efficiently
"From this article, create:
- 1 Twitter thread
- 5 LinkedIn posts
- 10 Substack notes"
```

### 6.3 Maintaining Voice Consistency

```
# Periodic check
"Review this post against my voice DNA. Does it sound like me?"

# Adjustment
"This is too formal. Make it match my voice DNA more closely"
```

### 6.4 Handling Writer's Block

```
# Get ideas
"Give me 10 content ideas about [topic] that would resonate with my ICP"

# Start with structure
"Give me an outline for a thought piece about [topic]"

# Brainstorm hooks
"Generate 5 different hooks for a post about [topic]"
```

### 6.5 Quality Control

```
# Pre-publish check
"Review this for:
- Voice consistency
- ICP targeting
- Grammar and clarity
- CTA strength"
```

---

## 7. Common Tasks Reference

### 7.1 Quick Reference Commands

| Task | Command |
|------|---------|
| LinkedIn post | "Write a LinkedIn post about [topic]" |
| Twitter thread | "Create a Twitter thread on [topic]" |
| Substack notes | "Write [N] Substack notes about [topic]" |
| Email sequence | "Create a [type] email sequence for [goal]" |
| Profile optimization | "Optimize my LinkedIn [section]" |
| Social bio | "Write a [platform] bio" |
| How-to guide | "Create a guide on how to [topic]" |
| Thought leadership | "Write a thought piece about [topic]" |

### 7.2 Profile Management Commands

| Task | Command |
|------|---------|
| Create voice DNA | "Help me create my voice DNA profile" |
| Update voice DNA | "Let's update my voice DNA" |
| Create ICP | "Help me create my ICP" |
| Create business profile | "Help me create my business profile" |
| Check profiles | "What do you know about me?" |

### 7.3 File Operations

| Task | Command |
|------|---------|
| Read file | "Read /knowledge/drafts/file.md" |
| Save content | "Save this to /knowledge/drafts/name.md" |
| Create folder | "Create a folder called [name] in knowledge" |
| List files | "What's in my drafts folder?" |

### 7.4 Troubleshooting Commands

| Issue | Command |
|-------|---------|
| Skills not working | "What skills are available?" |
| Voice mismatch | "Check this against my voice DNA" |
| Wrong audience | "Is this targeted at my ICP?" |
| Need frameworks | "What frameworks do you have for [content type]?" |

---

## Appendix: Keyboard Shortcuts

### Cursor Shortcuts

| Action | Windows/Linux | Mac |
|--------|---------------|-----|
| Open command palette | Ctrl+Shift+P | Cmd+Shift+P |
| Open file | Ctrl+P | Cmd+P |
| Save file | Ctrl+S | Cmd+S |
| Toggle sidebar | Ctrl+B | Cmd+B |

### Claude Code Panel

| Action | Method |
|--------|--------|
| Open Claude Code | Command Palette → "Claude Code: Open" |
| New chat | Click "+" in Claude panel |
| Clear chat | Type "/clear" |

---

*This manual is part of the AI Co-Writing System documentation suite.*
