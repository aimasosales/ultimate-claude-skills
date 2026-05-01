# System Architecture

**Version**: 1.0.0
**Last Updated**: 2025-01-01

---

## Table of Contents

1. [Architecture Overview](#1-architecture-overview)
2. [Component Architecture](#2-component-architecture)
3. [Data Architecture](#3-data-architecture)
4. [Execution Flow](#4-execution-flow)
5. [File System Structure](#5-file-system-structure)
6. [Integration Points](#6-integration-points)
7. [Design Decisions](#7-design-decisions)
8. [Scalability Considerations](#8-scalability-considerations)
9. [Security Considerations](#9-security-considerations)

---

## 1. Architecture Overview

### 1.1 High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              USER INTERFACE                                  │
│                    (Cursor / VS Code / Terminal)                            │
└─────────────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                              CLAUDE CODE                                     │
│                      (Anthropic's CLI / Extension)                          │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐             │
│  │ System Prompt   │  │ Skill Discovery │  │ Tool Execution  │             │
│  │ (claude.md)     │  │ Engine          │  │ Engine          │             │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘             │
└─────────────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           MY-WRITING-SYSTEM                                  │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                        CONFIGURATION LAYER                           │   │
│  │  ┌─────────────┐                                                    │   │
│  │  │ claude.md   │  System instructions, workflow rules, skill refs   │   │
│  │  └─────────────┘                                                    │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                          CONTEXT LAYER                               │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐         │   │
│  │  │ voice-dna   │  │    icp      │  │  business-profile   │         │   │
│  │  │   .json     │  │   .json     │  │       .json         │         │   │
│  │  └─────────────┘  └─────────────┘  └─────────────────────┘         │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                          SKILLS LAYER                                │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │   │
│  │  │linkedin- │ │twitter-  │ │substack- │ │thought-  │ │  ...     │  │   │
│  │  │  post    │ │ thread   │ │  note    │ │leadership│ │          │  │   │
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │                        KNOWLEDGE LAYER                               │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                  │   │
│  │  │   drafts/   │  │   notes/    │  │  archive/   │                  │   │
│  │  └─────────────┘  └─────────────┘  └─────────────┘                  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────────────┘
```

### 1.2 Architecture Principles

| Principle | Description |
|-----------|-------------|
| **Separation of Concerns** | Context, Skills, and Knowledge are independent layers |
| **Progressive Disclosure** | Information loaded only when needed |
| **Composability** | Skills can be combined for complex tasks |
| **Portability** | Folder-based, works across editors |
| **Extensibility** | Easy to add new skills and context types |

### 1.3 Design Philosophy

The architecture follows Alex McFarland's two-layer system concept:

1. **Production Layer** (Active)
   - Claude Code runtime
   - Skills execution
   - Context loading
   - Content generation

2. **Knowledge Layer** (Passive)
   - Content storage
   - Reference material
   - Learning corpus

---

## 2. Component Architecture

### 2.1 Component Hierarchy

```
my-writing-system/
│
├── claude.md                 [CONFIGURATION]
│   └── Defines system behavior, loads first
│
├── .claude/                  [RUNTIME]
│   ├── skills/              [SKILLS]
│   │   └── [11 skills]      Each skill is self-contained
│   └── agents/              [AGENTS - Future]
│       └── Reserved for autonomous workflows
│
├── context/                  [CONTEXT]
│   ├── voice-dna.json       Identity/voice
│   ├── icp.json             Audience
│   └── business-profile.json Business
│
└── knowledge/                [KNOWLEDGE]
    ├── drafts/              Work in progress
    ├── notes/               Ideas/research
    └── archive/             Published content
```

### 2.2 Component Responsibilities

#### claude.md (Configuration Component)
```
Responsibilities:
├── Define system identity
├── Specify component locations
├── Declare available skills
├── Set workflow rules
├── Establish expectations
└── Provide quick reference

Lifecycle:
├── Loaded: Every session start
├── Format: Markdown
└── Updates: Manual by user
```

#### Skills (Execution Components)
```
Responsibilities:
├── Package domain expertise
├── Define content frameworks
├── Provide step-by-step instructions
├── Include examples
└── Set quality standards

Lifecycle:
├── Discovery: Startup (name + description)
├── Loading: On-demand (full SKILL.md)
├── Format: YAML frontmatter + Markdown
└── Updates: Manual by user/developer
```

#### Context Profiles (State Components)
```
Responsibilities:
├── Store user identity (voice)
├── Define target audience (ICP)
├── Describe business context
└── Provide consistent reference

Lifecycle:
├── Loading: On-demand
├── Format: JSON (structured data)
└── Updates: Via creator skills or manual
```

#### Knowledge Base (Data Components)
```
Responsibilities:
├── Store work in progress
├── Archive published content
├── Provide reference material
└── Enable repurposing

Lifecycle:
├── Loading: On-demand
├── Format: Any text format
└── Updates: Continuous by user
```

### 2.3 Component Dependencies

```
                    claude.md
                        │
           ┌────────────┼────────────┐
           │            │            │
           ▼            ▼            ▼
        Skills ───► Context ◄─── Knowledge
           │            │            │
           └────────────┼────────────┘
                        │
                        ▼
                     Output
```

**Dependency Rules**:
- `claude.md` references all other components
- Skills read from Context
- Skills may read from Knowledge
- Context is independent
- Knowledge is independent

---

## 3. Data Architecture

### 3.1 Data Flow

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   Request    │───▶│   Process    │───▶│   Output     │
│              │    │              │    │              │
│ User prompt  │    │ Context +    │    │ Generated    │
│ Source file  │    │ Skills +     │    │ content      │
│              │    │ Knowledge    │    │              │
└──────────────┘    └──────────────┘    └──────────────┘
```

### 3.2 Data Formats

#### Configuration Data (Markdown)
```markdown
# claude.md structure
- Human-readable
- Supports formatting
- Easy to edit
- Version controllable
```

#### Context Data (JSON)
```json
{
  "profile_type": {
    "version": "1.0",
    "last_updated": "YYYY-MM-DD",
    "sections": {
      "key": "value"
    }
  }
}
```

**JSON Design Decisions**:
- Structured for AI parsing
- Nested for organization
- Includes metadata (version, date)
- Human-editable but optimized for AI

#### Skill Data (YAML + Markdown)
```yaml
---
name: lowercase-with-hyphens
description: Max 1024 characters
allowed-tools: Optional, comma-separated
---

# Markdown Content
Instructions, frameworks, examples
```

**Skill Format Decisions**:
- YAML frontmatter for metadata (machine-readable)
- Markdown body for instructions (human-readable)
- Progressive disclosure supported via file references

#### Knowledge Data (Any Text)
```
Supported formats:
├── .md (Markdown)
├── .txt (Plain text)
├── .json (Structured data)
└── .html (Scraped content)
```

### 3.3 Data Schemas

#### Voice DNA Schema
```json
{
  "$schema": "voice-dna-v1",
  "voice_dna": {
    "version": "string",
    "last_updated": "date",
    "core_essence": {
      "identity": "string",
      "primary_role": "string",
      "unique_angle": "string"
    },
    "personality_traits": {
      "primary": ["string"],
      "how_it_shows": {"trait": "description"}
    },
    "emotional_palette": {
      "dominant_emotions": ["string"],
      "emotional_range": {"emotion": "description"},
      "energy_level": "string"
    },
    "communication_style": {
      "formality": "string",
      "complexity": "string",
      "sentence_structure": {
        "preferred_length": "string",
        "patterns": ["string"]
      },
      "paragraph_style": "string"
    },
    "language_patterns": {
      "signature_phrases": ["string"],
      "power_words": ["string"],
      "words_to_avoid": ["string"],
      "transitions": ["string"]
    },
    "never_say": {
      "phrases": ["string"],
      "tones": ["string"],
      "approaches": ["string"]
    },
    "formatting_preferences": {
      "uses_emojis": "boolean",
      "uses_lists": "boolean",
      "uses_headers": "boolean",
      "uses_bold": "boolean"
    },
    "content_philosophy": {
      "core_belief": "string",
      "value_delivery": "string",
      "relationship_with_reader": "string"
    },
    "voice_examples": {
      "opening_lines": ["string"],
      "closing_lines": ["string"],
      "transitional_phrases": ["string"]
    }
  }
}
```

#### ICP Schema
```json
{
  "$schema": "icp-v1",
  "ideal_client_profile": {
    "version": "string",
    "last_updated": "date",
    "demographics": {
      "age_range": "string",
      "gender": "string",
      "location": "string",
      "income_level": "string",
      "education": "string"
    },
    "professional_profile": {
      "job_titles": ["string"],
      "industries": ["string"],
      "company_size": "string",
      "experience_level": "string",
      "decision_making_power": "string"
    },
    "psychographics": {
      "values": ["string"],
      "beliefs": ["string"],
      "personality_traits": ["string"]
    },
    "problems_and_pain_points": {
      "primary_problems": [{"problem": "string", "severity": "string", "frequency": "string"}],
      "frustrations": ["string"],
      "fears": ["string"]
    },
    "goals_and_desires": {
      "immediate_goals": ["string"],
      "long_term_aspirations": ["string"],
      "dream_outcome": "string"
    },
    "language_patterns": {
      "words_they_use": ["string"],
      "phrases_they_say": ["string"],
      "questions_they_ask": ["string"],
      "jargon_they_know": ["string"]
    },
    "content_consumption": {
      "platforms": ["string"],
      "content_formats": ["string"],
      "consumption_time": "string",
      "attention_span": "string"
    },
    "objections": {
      "common_objections": [{"objection": "string", "response": "string"}],
      "trust_barriers": ["string"]
    },
    "buying_triggers": {
      "emotional_triggers": ["string"],
      "logical_triggers": ["string"],
      "timing_triggers": ["string"]
    }
  }
}
```

#### Business Profile Schema
```json
{
  "$schema": "business-profile-v1",
  "business_profile": {
    "version": "string",
    "last_updated": "date",
    "company_overview": {
      "name": "string",
      "tagline": "string",
      "mission": "string",
      "vision": "string"
    },
    "value_proposition": {
      "primary_value": "string",
      "unique_mechanism": "string",
      "key_differentiators": ["string"]
    },
    "offerings": {
      "products": [{"name": "string", "type": "string", "description": "string", "price_point": "string", "ideal_for": "string"}],
      "services": [{"name": "string", "type": "string", "description": "string", "price_point": "string", "ideal_for": "string"}],
      "free_resources": [{"name": "string", "type": "string", "description": "string", "value": "string"}]
    },
    "positioning": {
      "market_position": "string",
      "competitor_comparison": "string",
      "category": "string",
      "niche_focus": "string"
    },
    "brand_voice_summary": {
      "personality": "string",
      "tone": "string",
      "values_demonstrated": ["string"]
    },
    "social_proof": {
      "key_metrics": ["string"],
      "testimonial_themes": ["string"],
      "notable_clients_or_features": ["string"]
    },
    "content_pillars": {
      "primary_topics": ["string"],
      "content_mission": "string",
      "content_style": "string"
    },
    "calls_to_action": {
      "primary_cta": {"action": "string", "url": "string", "when_to_use": "string"},
      "secondary_ctas": [{"action": "string", "when_to_use": "string"}]
    },
    "platforms": {
      "primary_platform": "string",
      "secondary_platforms": ["string"],
      "website": "string",
      "handles": {"platform": "handle"}
    }
  }
}
```

---

## 4. Execution Flow

### 4.1 Session Initialization

```
┌─────────────────────────────────────────────────────────────┐
│                    SESSION START                             │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 1. Claude Code loads claude.md from project root            │
│    - System identity established                            │
│    - Workflow rules loaded                                  │
│    - Skill references indexed                               │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Skill Discovery (Progressive Disclosure Level 1)         │
│    - Scan /.claude/skills/*/SKILL.md                       │
│    - Extract name + description from YAML frontmatter      │
│    - Index for matching against user requests              │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Ready for User Input                                     │
│    - Context files NOT loaded yet                          │
│    - Full skills NOT loaded yet                            │
│    - Minimal context footprint                             │
└─────────────────────────────────────────────────────────────┘
```

### 4.2 Request Processing

```
┌─────────────────────────────────────────────────────────────┐
│                    USER REQUEST                              │
│              "Write a LinkedIn post about AI"               │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 1. Request Analysis                                         │
│    - Parse user intent                                     │
│    - Match against skill descriptions                      │
│    - Identify: linkedin-post skill                         │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 2. Skill Loading (Progressive Disclosure Level 2)           │
│    - Read full /.claude/skills/linkedin-post/SKILL.md      │
│    - Parse frameworks and guidelines                       │
│    - Identify context requirements                         │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 3. Context Loading                                          │
│    - Read /context/voice-dna.json                          │
│    - Read /context/icp.json                                │
│    - Read /context/business-profile.json (if relevant)     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 4. Knowledge Reference (Optional)                           │
│    - Check if repurposing from existing content            │
│    - Load referenced files from /knowledge/                │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 5. Content Generation                                       │
│    - Apply voice DNA to output                             │
│    - Target ICP characteristics                            │
│    - Follow skill frameworks                               │
│    - Generate content                                      │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│ 6. Output Delivery                                          │
│    - Present formatted content                             │
│    - Explain choices made                                  │
│    - Offer alternatives if applicable                      │
└─────────────────────────────────────────────────────────────┘
```

### 4.3 Skill Invocation Flow

```
                    User Request
                         │
                         ▼
              ┌─────────────────────┐
              │ Match Skill by      │
              │ Description         │
              └─────────────────────┘
                         │
            ┌────────────┼────────────┐
            │            │            │
            ▼            ▼            ▼
       No Match    Single Match  Multiple Matches
            │            │            │
            ▼            ▼            ▼
       Ask User    Load Skill   Best Match or
       for clarity              Ask User
                         │
                         ▼
              ┌─────────────────────┐
              │ Read SKILL.md       │
              │ (Full content)      │
              └─────────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ Follow Instructions │
              │ Apply Frameworks    │
              └─────────────────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │ Generate Output     │
              └─────────────────────┘
```

---

## 5. File System Structure

### 5.1 Complete Directory Tree

```
my-writing-system/
│
├── claude.md                           # System instructions
│
├── .claude/                            # Claude Code configuration
│   │
│   ├── skills/                         # Skills directory
│   │   │
│   │   ├── business-profile-creator/
│   │   │   └── SKILL.md               # Business profile creation skill
│   │   │
│   │   ├── how-to-guide/
│   │   │   └── SKILL.md               # Tutorial/guide creation skill
│   │   │
│   │   ├── icp-creator/
│   │   │   └── SKILL.md               # ICP creation skill
│   │   │
│   │   ├── linkedin-post/
│   │   │   └── SKILL.md               # LinkedIn post skill
│   │   │
│   │   ├── linkedin-profile-optimizer/
│   │   │   └── SKILL.md               # LinkedIn optimization skill
│   │   │
│   │   ├── sales-email-sequence/
│   │   │   └── SKILL.md               # Email sequence skill
│   │   │
│   │   ├── social-media-bio-generator/
│   │   │   └── SKILL.md               # Bio generation skill
│   │   │
│   │   ├── substack-note/
│   │   │   └── SKILL.md               # Substack notes skill
│   │   │
│   │   ├── thought-leadership/
│   │   │   └── SKILL.md               # Thought leadership skill
│   │   │
│   │   ├── twitter-thread/
│   │   │   └── SKILL.md               # Twitter thread skill
│   │   │
│   │   └── voice-dna-creator/
│   │       └── SKILL.md               # Voice DNA creation skill
│   │
│   └── agents/                         # Agents directory (future)
│       └── .gitkeep                   # Placeholder
│
├── context/                            # Context profiles
│   ├── voice-dna.json                 # Voice/personality profile
│   ├── icp.json                       # Ideal client profile
│   └── business-profile.json          # Business context profile
│
├── knowledge/                          # Knowledge base
│   ├── drafts/                        # Work in progress
│   │   └── .gitkeep
│   ├── notes/                         # Ideas and research
│   │   └── .gitkeep
│   └── archive/                       # Published content
│       └── .gitkeep
│
├── docs/                               # Documentation
│   ├── DOCUMENTATION.md               # Main documentation
│   ├── ARCHITECTURE.md                # This file
│   ├── SKILLS-GUIDE.md                # Skills reference
│   ├── CONTEXT-PROFILES-GUIDE.md      # Profile guide
│   ├── USER-MANUAL.md                 # Usage guide
│   ├── TROUBLESHOOTING.md             # Problem solving
│   ├── CONTRIBUTING.md                # Contribution guide
│   └── CHANGELOG.md                   # Version history
│
└── README.md                           # Quick start guide
```

### 5.2 File Purposes

| File/Folder | Purpose | Edited By |
|-------------|---------|-----------|
| `claude.md` | System behavior configuration | User |
| `.claude/skills/` | Skill definitions | Developer/User |
| `context/*.json` | User context data | Creator skills/User |
| `knowledge/drafts/` | WIP content | User |
| `knowledge/notes/` | Research/ideas | User |
| `knowledge/archive/` | Published content | User |
| `docs/` | Documentation | Developer |
| `README.md` | Quick reference | Developer |

### 5.3 File Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Skills | lowercase-with-hyphens | `linkedin-post` |
| Context | lowercase-with-hyphens.json | `voice-dna.json` |
| Knowledge | YYYY-MM-DD_type_topic.md | `2025-01-15_newsletter_ai.md` |
| Docs | UPPERCASE.md | `ARCHITECTURE.md` |

---

## 6. Integration Points

### 6.1 Claude Code Integration

```
┌─────────────────────────────────────────────────────────────┐
│                     CLAUDE CODE                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Entry Points:                                              │
│  ├── claude.md (auto-loaded)                               │
│  ├── /.claude/skills/*/SKILL.md (discovered)               │
│  └── File system (read/write access)                       │
│                                                             │
│  Capabilities Used:                                         │
│  ├── File reading (context, knowledge)                     │
│  ├── File writing (save generated content)                 │
│  ├── Folder creation (organize outputs)                    │
│  └── Skill invocation (automatic)                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 6.2 Editor Integration

```
Cursor / VS Code
├── Claude Code Extension
│   ├── Panel for chat interface
│   ├── Permission prompts for file operations
│   └── Skill discovery
├── File Explorer
│   ├── Navigate project structure
│   └── Open/edit files
├── Markdown Preview
│   └── Preview generated content
└── Terminal (optional)
    └── Direct Claude Code CLI access
```

### 6.3 External Platform Integration

```
Output Destinations:
├── LinkedIn
│   ├── Posts (copy/paste)
│   └── Profile sections (copy/paste)
├── Twitter/X
│   └── Threads (copy/paste)
├── Substack
│   └── Notes (copy/paste)
├── Email Platforms
│   └── Sequences (copy/paste to ESP)
└── Websites/Blogs
    └── Articles (export markdown)
```

---

## 7. Design Decisions

### 7.1 Why JSON for Context Profiles?

**Decision**: Use JSON instead of YAML or Markdown for context profiles.

**Rationale**:
- Structured data optimized for AI parsing
- Clear hierarchy for nested information
- Easy to validate programmatically
- Standard format across programming ecosystems
- Human-editable when needed

**Trade-offs**:
- Less human-readable than YAML
- More verbose than some alternatives
- Requires valid syntax (no trailing commas)

### 7.2 Why Folder-Based Skills?

**Decision**: Each skill is a folder with SKILL.md, not a single file.

**Rationale**:
- Supports progressive disclosure (additional files)
- Allows bundled resources (scripts, templates)
- Clear organization
- Follows Anthropic's official specification

**Trade-offs**:
- More folders to manage
- Slightly more complex structure

### 7.3 Why Separate Knowledge Folders?

**Decision**: Three separate knowledge folders (drafts, notes, archive) instead of one.

**Rationale**:
- Clear content lifecycle (idea → draft → published)
- Different access patterns (drafts = frequent, archive = reference)
- Easier organization as content grows
- Intentional content management

**Trade-offs**:
- More folders to maintain
- Requires user discipline in organization

### 7.4 Why claude.md at Root?

**Decision**: Place system instructions at project root, not in .claude folder.

**Rationale**:
- Highly visible and easy to find
- Standard location for Claude Code
- First file users see
- Easy to edit

**Trade-offs**:
- Visible in file explorer (some prefer hidden)
- Could be accidentally modified

### 7.5 Why Model-Invoked Skills?

**Decision**: Skills are invoked automatically by Claude, not via slash commands.

**Rationale**:
- Lower friction for users
- Claude can combine skills intelligently
- No memorization of commands required
- Follows Anthropic's recommended pattern

**Trade-offs**:
- Less explicit control
- Requires clear skill descriptions

---

## 8. Scalability Considerations

### 8.1 Scaling Skills

**Current**: 11 skills
**Scalable to**: 50+ skills

**Considerations**:
- Skills are loaded on-demand (minimal overhead)
- Descriptions must be distinct to avoid confusion
- Organization: Consider subdirectories for many skills
```
.claude/skills/
├── content/
│   ├── linkedin-post/
│   └── twitter-thread/
├── profiles/
│   ├── voice-dna-creator/
│   └── icp-creator/
└── other/
```

### 8.2 Scaling Knowledge

**Current**: 3 folders
**Scalable to**: Thousands of files

**Considerations**:
- Use date-based subdirectories for large archives
- Claude can search with Grep/Glob tools
- Consider tagging in filenames
```
knowledge/archive/
├── 2024/
│   ├── q1/
│   └── q2/
└── 2025/
    └── q1/
```

### 8.3 Scaling Context

**Current**: 3 profiles
**Scalable to**: 10+ profiles

**Considerations**:
- Add profiles for specific use cases (product launches, campaigns)
- Keep core profiles focused
- Create profile variants for different audiences

### 8.4 Multi-User Scaling

**Current**: Single user system
**Scalable to**: Team usage

**Approach**:
- Version control with git
- Shared skills via repository
- Individual context profiles per user
- Shared knowledge base

---

## 9. Security Considerations

### 9.1 Data Security

**Sensitive Data Locations**:
- Context profiles (personal/business information)
- Knowledge base (proprietary content)

**Recommendations**:
- Do not commit sensitive context to public repos
- Use .gitignore for personal profiles
- Consider encryption for highly sensitive data

### 9.2 Skill Security

**Risks**:
- Malicious skills could execute harmful code
- Skills could exfiltrate data

**Mitigations**:
- Only use skills from trusted sources
- Review SKILL.md contents before use
- Use `allowed-tools` to restrict permissions
- Audit any scripts in skill folders

### 9.3 Git Security

**Recommended .gitignore**:
```
# Personal context (if sensitive)
context/voice-dna.json
context/business-profile.json

# API keys (never commit)
.env
*.key

# Personal knowledge
knowledge/notes/personal/

# Editor files
.vscode/
.cursor/
```

### 9.4 API Security

**If using API key**:
- Never commit API keys
- Use environment variables
- Rotate keys regularly
- Monitor usage for anomalies

---

*This architecture document is part of the AI Co-Writing System documentation suite.*
