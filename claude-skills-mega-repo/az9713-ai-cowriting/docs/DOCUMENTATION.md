# AI Co-Writing System - Complete Documentation

**Version**: 1.0.0
**Last Updated**: 2025-01-01
**Author**: Generated with Claude Code
**Based On**: Alex McFarland's Claude Code for Writing Masterclass

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Background & Motivation](#2-background--motivation)
3. [System Requirements](#3-system-requirements)
4. [Installation & Setup](#4-installation--setup)
5. [Core Concepts](#5-core-concepts)
6. [System Components](#6-system-components)
7. [Input/Output Specifications](#7-inputoutput-specifications)
8. [Usage Workflows](#8-usage-workflows)
9. [Customization Guide](#9-customization-guide)
10. [Best Practices](#10-best-practices)
11. [Glossary](#11-glossary)
12. [References](#12-references)

---

## 1. Project Overview

### 1.1 What Is This System?

The AI Co-Writing System is a Claude Code-based content creation framework that transforms Claude from a generic AI assistant into a personalized co-writer. It uses **context engineering** principles to produce content that matches your unique voice, targets your specific audience, and leverages reusable expertise (Skills).

### 1.2 Key Value Proposition

| Problem | Solution |
|---------|----------|
| Generic AI output | Voice DNA profiles capture your unique style |
| Inconsistent results | Persistent context loaded every session |
| Repetitive prompting | Skills package expertise for reuse |
| No audience targeting | ICP profiles define exactly who you write for |
| Starting from scratch | Knowledge base preserves content history |

### 1.3 Who Is This For?

- Newsletter creators (Substack, Beehive, ConvertKit)
- Social media content creators
- Ghostwriters and content writers
- Marketing teams and agencies
- Founders building personal brands
- Anyone scaling content production with AI

### 1.4 System Capabilities

The system can generate:
- LinkedIn posts and profile optimization
- Twitter/X threads
- Substack notes
- Thought leadership articles
- Email sequences
- Social media bios
- How-to guides and tutorials
- Custom content types (via new Skills)

---

## 2. Background & Motivation

### 2.1 The Problem with Traditional AI Writing

Traditional AI writing approaches suffer from:

1. **Lack of Context**: AI doesn't know who you are, your voice, or your audience
2. **Session Amnesia**: Every conversation starts from zero
3. **Prompt Dependency**: Quality depends on crafting perfect prompts each time
4. **Generic Output**: Content sounds like everyone else's AI-generated content
5. **No Expertise Capture**: Best practices aren't preserved or reusable

### 2.2 Context Engineering vs. Prompt Engineering

**Prompt Engineering** (Traditional):
```
Input: One-off prompt → Output: Generic content
Problems: Inconsistent, requires re-explaining, no memory
```

**Context Engineering** (This System):
```
Input: Structured context + Skills + Simple request
Output: Personalized, consistent content
Benefits: Persistent, reusable, voice-matched
```

### 2.3 The Formula

```
Context + Instructions = Quality Output
```

Where:
- **Context** = Voice DNA + ICP + Business Profile
- **Instructions** = Skills (packaged expertise)
- **Output** = Content that sounds like you, for your audience

### 2.4 Source Materials

This system was developed based on:

1. **Alex McFarland's Masterclass**: "Claude Code for Writing" video tutorial
2. **Anthropic's Agent Skills Documentation**: Official Claude Code skills specification
3. **Anthropic Engineering Blog**: "Equipping agents for the real world with Agent Skills"

---

## 3. System Requirements

### 3.1 Software Requirements

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| Claude Code | v1.0+ | Latest |
| Code Editor | Any with Claude Code support | Cursor |
| Operating System | Windows/macOS/Linux | Any |

### 3.2 Account Requirements

**Option A: Claude Subscription (Recommended)**
- Claude Pro ($20/month), Team ($100/month), or Max ($200/month)
- Connected via Claude Code authentication
- Best for: Heavy usage, predictable costs

**Option B: API Key**
- Anthropic API account with credits
- Pay-per-use pricing
- Best for: Light usage, experimentation

### 3.3 Editor Setup (Cursor)

1. Download Cursor from https://cursor.sh
2. Install "Claude Code for VS Code" extension
3. Authenticate with Claude subscription or API key
4. Open the `my-writing-system` folder

### 3.4 Knowledge Prerequisites

Users should understand:
- Basic file/folder navigation
- Markdown format basics
- JSON structure basics (for context profiles)

---

## 4. Installation & Setup

### 4.1 Quick Start (5 Minutes)

```bash
# 1. Copy the my-writing-system folder to your desired location
# 2. Open in Cursor or VS Code with Claude Code extension
# 3. Claude automatically loads claude.md on startup
# 4. Start with: "Help me create my voice DNA profile"
```

### 4.2 Detailed Setup Process

#### Step 1: Folder Placement
Place `my-writing-system/` anywhere on your computer. Recommended locations:
- `~/Documents/my-writing-system/`
- `~/Projects/my-writing-system/`

#### Step 2: Open in Editor
```
Cursor → File → Open Folder → Select my-writing-system
```

#### Step 3: Verify Claude Code Connection
In Claude Code panel, type:
```
What skills are available?
```
Claude should list all 11 skills.

#### Step 4: Create Context Profiles
Run each creator skill in order:

1. **Voice DNA** (Most Important)
   ```
   Help me create my voice DNA profile
   ```
   - Provide 3-10 writing samples
   - Answer analysis questions
   - Review and refine output

2. **ICP (Ideal Client Profile)**
   ```
   Help me create my ICP
   ```
   - Complete the interview
   - Be specific about your audience
   - Save to `/context/icp.json`

3. **Business Profile**
   ```
   Help me create my business profile
   ```
   - Answer business questions
   - Include offerings and positioning
   - Save to `/context/business-profile.json`

#### Step 5: Add Knowledge (Optional but Recommended)
Copy your best content to `/knowledge/archive/`:
- Past newsletters
- Published articles
- Social media content

### 4.3 Verification Checklist

- [ ] Folder opens in editor without errors
- [ ] Claude Code extension is active
- [ ] `claude.md` is present in root
- [ ] All 11 skill folders exist in `/.claude/skills/`
- [ ] Context folder has 3 JSON files
- [ ] Knowledge folders exist (even if empty)

---

## 5. Core Concepts

### 5.1 Context Engineering

**Definition**: The practice of providing AI with structured, persistent context rather than relying on one-off prompts.

**Four Pillars**:

1. **Structured Information**: Organized profiles, not random text dumps
2. **Persistent Files**: Context that exists in the project, always available
3. **Reusable Instructions**: Skills written once, used forever
4. **System Prompts**: Rules defining AI behavior (`claude.md`)

### 5.2 Progressive Disclosure

Skills use a three-level disclosure system:

```
Level 1: Name + Description (loaded at startup, minimal context)
    ↓
Level 2: Full SKILL.md (loaded when skill is triggered)
    ↓
Level 3: Supporting files (loaded only when needed)
```

**Why it matters**: Claude doesn't waste context window on irrelevant information.

### 5.3 Model-Invoked vs. User-Invoked

| Type | Trigger | Example |
|------|---------|---------|
| **Model-Invoked** (Skills) | Claude decides automatically | "Write a LinkedIn post" → Claude invokes `linkedin-post` skill |
| **User-Invoked** (Slash Commands) | User types explicit command | `/review-code` |

Skills are model-invoked—Claude autonomously decides when to use them based on your request.

### 5.4 The Two-Layer System

**Layer 1: Production Layer**
- Where content gets made
- Components: Claude Code, Skills, Context Profiles
- Action: Writing, generating, creating

**Layer 2: Knowledge Layer**
- Where thinking lives
- Components: Drafts, Notes, Archive
- Action: Storing, referencing, learning

---

## 6. System Components

### 6.1 Component Overview

```
my-writing-system/
├── claude.md                    # SYSTEM: Auto-loaded instructions
├── .claude/
│   ├── skills/                  # SKILLS: Packaged expertise
│   │   └── [11 skill folders]
│   └── agents/                  # AGENTS: Future autonomous workflows
├── context/                     # CONTEXT: Who you are
│   ├── voice-dna.json
│   ├── icp.json
│   └── business-profile.json
└── knowledge/                   # KNOWLEDGE: Your content brain
    ├── drafts/
    ├── notes/
    └── archive/
```

### 6.2 claude.md (System Instructions)

**Purpose**: Master instructions that define how Claude operates in your system.

**Location**: `/claude.md` (root of project)

**Behavior**: Automatically loaded at every Claude Code session startup.

**Contents**:
- System identity and role
- Architecture overview
- Context profile locations
- Available skills list
- Workflow instructions
- Expectations and rules

**Modification**: Users should customize this file for their specific needs.

### 6.3 Context Profiles

#### voice-dna.json
**Purpose**: Captures your unique writing voice, tone, and personality.

**Key Sections**:
- `core_essence`: Identity, role, unique angle
- `personality_traits`: Primary traits and how they show
- `emotional_palette`: Dominant emotions, energy level
- `communication_style`: Formality, complexity, sentence patterns
- `language_patterns`: Signature phrases, power words, transitions
- `never_say`: Phrases, tones, and approaches to avoid
- `formatting_preferences`: Emoji use, lists, headers, bold
- `voice_examples`: Sample openings, closings, transitions

#### icp.json
**Purpose**: Defines your ideal client/reader profile.

**Key Sections**:
- `demographics`: Age, gender, location, income, education
- `professional_profile`: Job titles, industries, experience
- `psychographics`: Values, beliefs, personality traits
- `problems_and_pain_points`: Primary problems, frustrations, fears
- `goals_and_desires`: Immediate goals, long-term aspirations
- `language_patterns`: Words they use, questions they ask
- `content_consumption`: Platforms, formats, timing
- `objections`: Common objections, trust barriers
- `buying_triggers`: Emotional, logical, timing triggers

#### business-profile.json
**Purpose**: Describes your business, offerings, and positioning.

**Key Sections**:
- `company_overview`: Name, tagline, mission, vision
- `value_proposition`: Primary value, unique mechanism, differentiators
- `offerings`: Products, services, free resources
- `positioning`: Market position, category, niche
- `brand_voice_summary`: Personality, tone, values
- `social_proof`: Metrics, testimonials, features
- `content_pillars`: Primary topics, content mission
- `calls_to_action`: Primary and secondary CTAs
- `platforms`: Social handles and websites

### 6.4 Skills

**Definition**: Packaged expertise stored as folders containing `SKILL.md` files.

**Location**: `/.claude/skills/[skill-name]/SKILL.md`

**Format Requirements**:
```yaml
---
name: skill-name-lowercase-with-hyphens
description: Brief description (max 1024 chars). Include what it does AND when to use it.
---

# Skill Title

[Markdown content with instructions, frameworks, examples]
```

**Available Skills**:

| Skill | Input | Output |
|-------|-------|--------|
| `voice-dna-creator` | Writing samples | Voice DNA JSON |
| `icp-creator` | Interview answers | ICP JSON |
| `business-profile-creator` | Interview answers | Business profile JSON |
| `linkedin-post` | Topic/content | LinkedIn post |
| `linkedin-profile-optimizer` | Current profile | Optimized sections |
| `twitter-thread` | Topic/content | Twitter thread |
| `substack-note` | Topic/content | Substack note(s) |
| `thought-leadership` | Topic/angle | Long-form article |
| `sales-email-sequence` | Offer/goal | Email sequence |
| `social-media-bio-generator` | Platform/info | Platform bio |
| `how-to-guide` | Topic/process | Tutorial/guide |

### 6.5 Knowledge Base

**Purpose**: Store your content for reference, repurposing, and learning.

**Structure**:

```
knowledge/
├── drafts/      # Work in progress
├── notes/       # Ideas, research, transcripts
└── archive/     # Published content
```

**Usage by Claude**:
- Reference past content for voice consistency
- Repurpose existing content into new formats
- Avoid repeating the same ideas
- Learn from your best-performing content

---

## 7. Input/Output Specifications

### 7.1 System Inputs

#### Primary Inputs

| Input Type | Format | Location | Required |
|------------|--------|----------|----------|
| System Instructions | Markdown | `/claude.md` | Yes |
| Voice DNA | JSON | `/context/voice-dna.json` | Yes |
| ICP | JSON | `/context/icp.json` | Recommended |
| Business Profile | JSON | `/context/business-profile.json` | Recommended |
| Skills | Markdown with YAML | `/.claude/skills/*/SKILL.md` | Yes |
| Knowledge | Any text format | `/knowledge/*` | Optional |

#### User Request Inputs

| Request Type | Example | Skills Invoked |
|--------------|---------|----------------|
| Content creation | "Write a LinkedIn post about AI" | `linkedin-post` |
| Profile creation | "Help me create my voice DNA" | `voice-dna-creator` |
| Batch generation | "Write 20 Substack notes" | `substack-note` |
| Optimization | "Optimize my LinkedIn headline" | `linkedin-profile-optimizer` |
| Repurposing | "Turn this newsletter into a thread" | `twitter-thread` |

### 7.2 System Outputs

#### Content Outputs

| Output Type | Format | Typical Length |
|-------------|--------|----------------|
| LinkedIn post | Plain text | 1,200-3,000 chars |
| Twitter thread | Numbered tweets | 7-15 tweets × 280 chars |
| Substack note | Plain text | 280-1,000 chars |
| Thought leadership | Markdown | 1,000-5,000 words |
| Email sequence | Structured emails | 5-10 emails |
| Social bio | Plain text | Platform-specific limits |
| How-to guide | Markdown | 500-5,000 words |

#### Profile Outputs

| Output Type | Format | Location |
|-------------|--------|----------|
| Voice DNA | JSON | `/context/voice-dna.json` |
| ICP | JSON | `/context/icp.json` |
| Business Profile | JSON | `/context/business-profile.json` |

### 7.3 Data Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        USER REQUEST                              │
│                   "Write a LinkedIn post"                        │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      CLAUDE CODE                                 │
│  1. Load claude.md (system instructions)                        │
│  2. Parse user request                                          │
│  3. Identify relevant skill (linkedin-post)                     │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    CONTEXT LOADING                               │
│  1. Read /context/voice-dna.json                                │
│  2. Read /context/icp.json                                      │
│  3. Read /context/business-profile.json                         │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    SKILL INVOCATION                              │
│  1. Load /.claude/skills/linkedin-post/SKILL.md                 │
│  2. Follow frameworks and guidelines                            │
│  3. Apply voice DNA to output                                   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    KNOWLEDGE REFERENCE                           │
│  (Optional) Check /knowledge/ for:                              │
│  - Related past content                                         │
│  - Source material to repurpose                                 │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                        OUTPUT                                    │
│  - Content matching voice DNA                                   │
│  - Targeted to ICP                                              │
│  - Following skill guidelines                                   │
│  - Ready for publishing                                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## 8. Usage Workflows

### 8.1 Initial Setup Workflow

```
Day 1: System Setup
├── 1. Open folder in Cursor
├── 2. Verify Claude Code connection
├── 3. Create Voice DNA (30-60 min)
│   ├── Gather 3-10 writing samples
│   ├── Run voice-dna-creator skill
│   └── Review and refine output
├── 4. Create ICP (15-30 min)
│   ├── Run icp-creator skill
│   ├── Answer interview questions
│   └── Save output
└── 5. Create Business Profile (15-30 min)
    ├── Run business-profile-creator skill
    ├── Answer interview questions
    └── Save output

Day 2+: Add Knowledge
├── Copy published newsletters to /knowledge/archive/
├── Add content ideas to /knowledge/notes/
└── Organize by content type
```

### 8.2 Daily Writing Workflow

```
Daily Content Creation
├── 1. Open project in Cursor
├── 2. Claude loads claude.md automatically
├── 3. Request content
│   ├── Simple: "Write a LinkedIn post about [topic]"
│   ├── Batch: "Write 10 Substack notes from my latest newsletter"
│   └── Repurpose: "Turn this article into a Twitter thread"
├── 4. Review output
├── 5. Request adjustments if needed
├── 6. Copy to publishing platform
└── 7. (Optional) Save to /knowledge/archive/
```

### 8.3 Content Repurposing Workflow

```
Repurposing Long-Form Content
├── 1. Save newsletter/article to /knowledge/drafts/
├── 2. Request repurposing:
│   ├── "Write 20 Substack notes from my latest newsletter"
│   ├── "Create a Twitter thread from this article"
│   └── "Generate 5 LinkedIn posts from this content"
├── 3. Review batch output
├── 4. Edit/customize as needed
└── 5. Schedule across platforms
```

### 8.4 Profile Optimization Workflow

```
Profile Optimization
├── 1. Gather current profile content
├── 2. Request optimization:
│   └── "Optimize my LinkedIn profile"
├── 3. Claude analyzes against ICP and business profile
├── 4. Receive optimized sections
├── 5. Review alternatives provided
└── 6. Update profiles on platforms
```

---

## 9. Customization Guide

### 9.1 Customizing claude.md

**When to modify**:
- Adding new skills
- Changing workflow rules
- Adding project-specific instructions
- Modifying expectations

**How to modify**:
```markdown
# Add new skills to the Skills Guide table
| new-skill | Use when [trigger] |

# Add new workflow rules
## Custom Rules
- [Your rule here]
- [Your rule here]
```

### 9.2 Creating New Skills

**Step 1**: Create skill folder
```bash
mkdir -p .claude/skills/my-new-skill
```

**Step 2**: Create SKILL.md
```markdown
---
name: my-new-skill
description: What it does. When to use it.
---

# My New Skill

## Instructions
[How Claude should use this skill]

## Examples
[Concrete examples]
```

**Step 3**: Update claude.md
Add the skill to the skills table.

**Step 4**: Test
```
Test my new skill for [use case]
```

### 9.3 Extending Context Profiles

**Adding new profile types**:
1. Create new JSON file in `/context/`
2. Reference it in `claude.md`
3. Create creator skill if needed

**Example: Adding a Product Profile**
```json
// /context/product-profile.json
{
  "product_profile": {
    "name": "Product Name",
    "description": "...",
    "features": [],
    "benefits": [],
    "pricing": {}
  }
}
```

### 9.4 Organizing Knowledge Base

**Recommended structure for heavy users**:
```
knowledge/
├── drafts/
│   ├── newsletters/
│   ├── articles/
│   └── social/
├── notes/
│   ├── ideas/
│   ├── research/
│   └── transcripts/
└── archive/
    ├── 2024/
    ├── 2025/
    └── by-topic/
```

---

## 10. Best Practices

### 10.1 Voice DNA Best Practices

- **Use diverse samples**: Include different content types
- **Update regularly**: Refine as your voice evolves
- **Focus on tone, not just words**: Capture personality, not phrases
- **Include what NOT to say**: Equally important as what to say

### 10.2 Skills Best Practices

- **Specific descriptions**: Include WHAT and WHEN
- **Actionable instructions**: Step-by-step, not vague
- **Include examples**: Show, don't just tell
- **Test thoroughly**: Verify skill triggers correctly

### 10.3 Content Generation Best Practices

- **Be specific in requests**: "LinkedIn post about AI writing tools" not "write something"
- **Provide source material**: For repurposing, point to specific files
- **Review before publishing**: AI is co-writer, not replacement
- **Give feedback**: Help Claude learn your preferences

### 10.4 System Maintenance Best Practices

- **Regular profile updates**: Quarterly voice DNA review
- **Archive published content**: Build knowledge base over time
- **Version control**: Use git for tracking changes
- **Backup context files**: Critical for continuity

---

## 11. Glossary

| Term | Definition |
|------|------------|
| **Agent Skills** | Modular capabilities packaged as folders with SKILL.md files |
| **Claude Code** | Anthropic's CLI tool for AI-assisted development and writing |
| **Context Engineering** | Practice of providing structured, persistent context to AI |
| **Context Profile** | JSON file containing structured information (voice, ICP, business) |
| **ICP** | Ideal Client Profile - detailed description of target audience |
| **Knowledge Base** | Collection of content for reference and repurposing |
| **Model-Invoked** | Triggered automatically by Claude based on context |
| **Progressive Disclosure** | Loading information in levels (metadata → full skill → supporting files) |
| **Skill** | Packaged expertise that Claude can invoke for specific tasks |
| **System Prompt** | Instructions in claude.md that define Claude's behavior |
| **User-Invoked** | Triggered explicitly by user action (slash commands) |
| **Voice DNA** | Profile capturing unique writing voice and personality |

---

## 12. References

### 12.1 Source Materials

1. **Alex McFarland's Masterclass**
   - Title: "Claude Code Masterclass: Build Your AI Co-Writing System"
   - Platform: YouTube / Substack (AI WriterOps)
   - URL: https://www.youtube.com/watch?v=Ip566JVP_30&t=1s

2. **Anthropic Agent Skills Documentation**
   - URL: https://code.claude.com/docs/en/skills
   - Topics: Creating, managing, and sharing Skills

3. **Anthropic Engineering Blog**
   - Title: "Equipping agents for the real world with Agent Skills"
   - URL: https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills

### 12.2 Related Documentation

- [ARCHITECTURE.md](./ARCHITECTURE.md) - Technical architecture details
- [SKILLS-GUIDE.md](./SKILLS-GUIDE.md) - Complete skills reference
- [CONTEXT-PROFILES-GUIDE.md](./CONTEXT-PROFILES-GUIDE.md) - Profile creation guide
- [USER-MANUAL.md](./USER-MANUAL.md) - Day-to-day usage guide
- [TROUBLESHOOTING.md](./TROUBLESHOOTING.md) - Common issues and solutions
- [CONTRIBUTING.md](./CONTRIBUTING.md) - How to contribute improvements
- [CHANGELOG.md](./CHANGELOG.md) - Version history

### 12.3 External Resources

- Claude Code Documentation: https://code.claude.com/docs
- Cursor Editor: https://cursor.sh
- Anthropic: https://anthropic.com

---

*This documentation is part of the AI Co-Writing System. For questions or improvements, see CONTRIBUTING.md.*
