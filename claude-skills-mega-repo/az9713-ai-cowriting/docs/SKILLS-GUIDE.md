# Skills Development Guide

**Version**: 1.0.0
**Last Updated**: 2025-01-01

---

## Table of Contents

1. [Understanding Skills](#1-understanding-skills)
2. [Skill Specification](#2-skill-specification)
3. [Available Skills Reference](#3-available-skills-reference)
4. [Creating New Skills](#4-creating-new-skills)
5. [Skill Best Practices](#5-skill-best-practices)
6. [Testing Skills](#6-testing-skills)
7. [Troubleshooting Skills](#7-troubleshooting-skills)

---

## 1. Understanding Skills

### 1.1 What Are Skills?

Skills are **packaged expertise** that extend Claude's capabilities for specific tasks. Each skill is a folder containing a `SKILL.md` file with instructions, frameworks, and examples that Claude reads when the skill is relevant to your request.

### 1.2 How Skills Work

```
┌─────────────────────────────────────────────────────────────┐
│                    SKILL LIFECYCLE                           │
└─────────────────────────────────────────────────────────────┘

1. DISCOVERY (Startup)
   └── Claude reads name + description from all SKILL.md files
   └── Indexes skills for matching

2. MATCHING (User Request)
   └── Claude matches request to skill description
   └── Example: "Write a LinkedIn post" → linkedin-post skill

3. LOADING (On-demand)
   └── Full SKILL.md content loaded into context
   └── Supporting files loaded if referenced

4. EXECUTION
   └── Claude follows skill instructions
   └── Applies frameworks and guidelines
   └── Generates output
```

### 1.3 Model-Invoked vs User-Invoked

| Type | Trigger | Example |
|------|---------|---------|
| **Model-Invoked** (Skills) | Automatic based on request | "Write a tweet" → Claude selects twitter-thread |
| **User-Invoked** (Commands) | Explicit slash command | /summarize |

**Skills are model-invoked** - Claude autonomously decides when to use them.

### 1.4 Progressive Disclosure

Skills use a three-level disclosure system to manage context efficiently:

```
Level 1: Metadata Only (Always Loaded)
├── name: linkedin-post
└── description: Create engaging LinkedIn posts...

Level 2: Full Skill (Loaded When Invoked)
├── All SKILL.md content
├── Instructions
├── Frameworks
└── Examples

Level 3: Supporting Files (Loaded When Needed)
├── reference.md
├── examples.md
└── scripts/helper.py
```

---

## 2. Skill Specification

### 2.1 File Structure

```
skill-name/
├── SKILL.md           # Required: Main skill file
├── reference.md       # Optional: Additional documentation
├── examples.md        # Optional: Extended examples
└── scripts/           # Optional: Helper scripts
    └── helper.py
```

### 2.2 SKILL.md Format

```yaml
---
name: skill-name-here
description: What the skill does. When Claude should use it. Max 1024 characters.
allowed-tools: Read, Grep, Glob  # Optional: Restrict available tools
---

# Skill Title

## Section 1
Content...

## Section 2
Content...
```

### 2.3 Frontmatter Fields

| Field | Required | Type | Constraints |
|-------|----------|------|-------------|
| `name` | Yes | String | Lowercase, hyphens, max 64 chars |
| `description` | Yes | String | Max 1024 characters |
| `allowed-tools` | No | String | Comma-separated tool names |

### 2.4 Name Requirements

**Valid names**:
- `linkedin-post`
- `voice-dna-creator`
- `how-to-guide-v2`

**Invalid names**:
- `LinkedIn Post` (uppercase, spaces)
- `my_skill` (underscores)
- `a-very-long-skill-name-that-exceeds-the-sixty-four-character-maximum-limit` (too long)

### 2.5 Description Requirements

The description is **critical** for skill discovery. It must include:
1. **What** the skill does
2. **When** Claude should use it

**Good description**:
```yaml
description: Create engaging LinkedIn posts that drive engagement and build authority. Use when the user wants to write LinkedIn content, needs posts for their LinkedIn strategy, or wants to repurpose content for LinkedIn.
```

**Poor description**:
```yaml
description: Helps with LinkedIn
```

---

## 3. Available Skills Reference

### 3.1 Content Creator Skills

#### voice-dna-creator
```yaml
name: voice-dna-creator
description: Analyze writing samples to create a comprehensive voice DNA profile.
```
**Input**: 3-10 writing samples
**Output**: JSON voice profile
**Use When**: Setting up system, creating client profiles

---

#### icp-creator
```yaml
name: icp-creator
description: Create detailed Ideal Client Profile through guided interview.
```
**Input**: Interview answers
**Output**: JSON ICP profile
**Use When**: Defining target audience

---

#### business-profile-creator
```yaml
name: business-profile-creator
description: Create comprehensive business context profiles through guided interview.
```
**Input**: Interview answers
**Output**: JSON business profile
**Use When**: Setting up business context

---

### 3.2 Content Generation Skills

#### linkedin-post
```yaml
name: linkedin-post
description: Create engaging LinkedIn posts that drive engagement and build authority.
```
**Input**: Topic or content to repurpose
**Output**: LinkedIn post with hook, body, CTA
**Frameworks**: Hook→Story→Lesson→CTA, Contrarian, List, Before/After, How-To

---

#### twitter-thread
```yaml
name: twitter-thread
description: Create viral Twitter/X threads that educate, entertain, and grow your audience.
```
**Input**: Topic or content to repurpose
**Output**: 7-15 tweet thread
**Frameworks**: How-To, Story, Listicle, Contrarian, Case Study, Breakdown

---

#### substack-note
```yaml
name: substack-note
description: Generate high-performing Substack notes that drive engagement.
```
**Input**: Topic or content to repurpose
**Output**: Short-form Substack note(s)
**Frameworks**: Observation, Contrarian, Quick Tip, Story, Question, Behind-the-Scenes

---

#### thought-leadership
```yaml
name: thought-leadership
description: Create thought leadership content including long-form articles and essays.
```
**Input**: Topic and perspective
**Output**: Long-form article (1,000-5,000 words)
**Types**: Perspective Piece, Framework, Prediction, Lessons, State of Industry

---

#### how-to-guide
```yaml
name: how-to-guide
description: Create comprehensive how-to guides and tutorials.
```
**Input**: Topic/process to explain
**Output**: Step-by-step guide
**Types**: Quick Tutorial, Comprehensive Guide, Ultimate Guide

---

#### sales-email-sequence
```yaml
name: sales-email-sequence
description: Create high-converting email sequences for sales, launches, and nurture.
```
**Input**: Offer details, sequence type, timeline
**Output**: Multi-email sequence
**Types**: Welcome (5-7), Launch (7-10), Nurture (ongoing), Re-engagement (3-5)

---

### 3.3 Optimization Skills

#### linkedin-profile-optimizer
```yaml
name: linkedin-profile-optimizer
description: Optimize LinkedIn profile sections for maximum impact and conversions.
```
**Input**: Current profile content
**Output**: Optimized headline, about, experience, etc.
**Sections**: Headline, About, Featured, Experience, Skills, Recommendations

---

#### social-media-bio-generator
```yaml
name: social-media-bio-generator
description: Create compelling social media bios for any platform.
```
**Input**: Platform, goal, credentials
**Output**: Platform-optimized bio
**Platforms**: Twitter (160), Instagram (150), LinkedIn (220), TikTok (80), YouTube (1000)

---

## 4. Creating New Skills

### 4.1 Step-by-Step Process

#### Step 1: Identify the Need
- What content type is missing?
- What task do you repeat often?
- What expertise should be packaged?

#### Step 2: Create Folder Structure
```bash
mkdir -p .claude/skills/my-new-skill
```

#### Step 3: Write SKILL.md

```yaml
---
name: my-new-skill
description: Clear description of what this does. Specific triggers for when to use it.
---

# My New Skill

## When to Use This Skill
- Trigger condition 1
- Trigger condition 2

## Before Writing
1. Read context profiles
2. Check for source material

## Instructions
Step-by-step instructions...

## Frameworks
### Framework 1: Name
```
Template structure...
```

## Examples
Concrete examples...

## Output Format
How output should be structured...

## Quality Checklist
- [ ] Check 1
- [ ] Check 2
```

#### Step 4: Update claude.md
Add skill to the skills table in system instructions.

#### Step 5: Test
Request content that should trigger the skill.

### 4.2 Skill Template

```yaml
---
name: skill-name
description: [What it does]. Use when [triggers].
---

# Skill Name

## When to Use This Skill
- [Condition 1]
- [Condition 2]

## Before Writing

1. **Read context profiles**:
   - `/context/voice-dna.json` - Match voice
   - `/context/icp.json` - Target audience
   - `/context/business-profile.json` - Reference offerings

2. **Check for source material** in `/knowledge/`

## Instructions

[Step-by-step instructions for Claude]

## Frameworks

### Framework 1: [Name]
```
[Template structure]
```

### Framework 2: [Name]
```
[Template structure]
```

## Writing Guidelines

### [Category]
- [Guideline 1]
- [Guideline 2]

### What to Avoid
- [Anti-pattern 1]
- [Anti-pattern 2]

## Output Format

[How output should be structured]

## Examples

### Example 1: [Type]
```
[Concrete example]
```

## Quality Checklist

Before delivering:
- [ ] [Check 1]
- [ ] [Check 2]
- [ ] [Check 3]
```

### 4.3 Multi-File Skills

For complex skills, split content across files:

```
complex-skill/
├── SKILL.md           # Main instructions (keep lean)
├── frameworks.md      # Detailed frameworks
├── examples.md        # Extended examples
└── reference.md       # API/reference documentation
```

**In SKILL.md, reference other files**:
```markdown
For detailed frameworks, see [frameworks.md](frameworks.md).
For extended examples, see [examples.md](examples.md).
```

Claude will load these files only when needed (Level 3 progressive disclosure).

---

## 5. Skill Best Practices

### 5.1 Description Best Practices

| Do | Don't |
|----|-------|
| Include what AND when | Just describe what |
| Use specific trigger words | Use vague language |
| Mention content types | Assume Claude knows |
| Stay under 1024 chars | Write paragraphs |

**Example transformation**:

```yaml
# Poor
description: Helps with social media

# Better
description: Create Twitter/X threads that educate and grow your audience. Use when writing threads, breaking down complex topics, or repurposing long-form content into thread format.
```

### 5.2 Instruction Best Practices

| Do | Don't |
|----|-------|
| Be specific and actionable | Be vague |
| Provide frameworks | Just say "write well" |
| Include examples | Assume understanding |
| Reference context profiles | Ignore personalization |
| Include quality checks | Skip validation |

### 5.3 Framework Best Practices

- **Name frameworks clearly**: Hook→Story→Lesson→CTA
- **Provide templates**: Show structure visually
- **Explain when to use each**: Different frameworks for different needs
- **Include examples**: Show frameworks in action

### 5.4 Organization Best Practices

- **One skill, one capability**: Don't combine unrelated tasks
- **Clear boundaries**: Skills shouldn't overlap significantly
- **Consistent structure**: Use similar sections across skills
- **Maintain context awareness**: Always reference context profiles

---

## 6. Testing Skills

### 6.1 Testing Checklist

- [ ] Skill is discovered (check with "What skills are available?")
- [ ] Skill triggers on expected requests
- [ ] Skill reads context profiles
- [ ] Output follows frameworks
- [ ] Output matches voice DNA
- [ ] Quality checklist items are met

### 6.2 Test Commands

```
# Test discovery
"What skills are available?"

# Test specific trigger
"Write a [content type that should trigger skill]"

# Test with context
"Write a LinkedIn post about AI" (should use voice DNA)

# Test alternatives
"I need help with LinkedIn content" (less explicit, should still trigger)
```

### 6.3 Debugging Skill Issues

**Skill not triggering**:
1. Check description is specific enough
2. Verify YAML syntax is valid
3. Check skill is in correct location
4. Run Claude with `--debug` flag

**Wrong output**:
1. Check instructions are clear
2. Verify frameworks are being followed
3. Ensure context profiles are being read
4. Check examples match expected output

---

## 7. Troubleshooting Skills

### 7.1 Common Issues

#### Issue: Skill Not Found
```
Symptoms: Claude doesn't recognize skill
Causes:
- SKILL.md not in correct location
- Invalid YAML frontmatter
- Missing name or description
Solutions:
- Verify path: .claude/skills/skill-name/SKILL.md
- Check YAML syntax
- Ensure frontmatter has --- delimiters
```

#### Issue: Skill Not Triggering
```
Symptoms: Claude doesn't use skill when expected
Causes:
- Description too vague
- Trigger words not matching user request
- Another skill has similar description
Solutions:
- Make description more specific
- Include explicit trigger phrases
- Differentiate from similar skills
```

#### Issue: Wrong Output Format
```
Symptoms: Output doesn't match expected format
Causes:
- Instructions not clear
- Missing output format section
- Frameworks not specific enough
Solutions:
- Add explicit output format section
- Include concrete examples
- Be prescriptive about structure
```

#### Issue: Voice Not Matching
```
Symptoms: Output sounds generic, not personalized
Causes:
- Skill not reading voice DNA
- Instructions don't reference context
- Context files not populated
Solutions:
- Add "Read context profiles" to instructions
- Explicitly mention voice DNA in workflow
- Verify context files exist and are populated
```

### 7.2 Validation Commands

```bash
# Check YAML syntax
cat .claude/skills/my-skill/SKILL.md | head -n 10

# List all skills
ls .claude/skills/*/SKILL.md

# Check skill content
cat .claude/skills/my-skill/SKILL.md
```

### 7.3 Debug Mode

Run Claude Code with debug flag to see skill loading:
```bash
claude --debug
```

---

## Appendix A: Skill Ideas

### Content Skills Not Yet Implemented

| Skill | Purpose |
|-------|---------|
| `newsletter-writer` | Full newsletter creation |
| `blog-post` | SEO-optimized blog posts |
| `youtube-script` | Video scripts |
| `podcast-outline` | Podcast episode outlines |
| `case-study` | Customer case studies |
| `press-release` | PR announcements |
| `landing-page-copy` | Conversion copy |
| `ad-copy` | Advertising copy |

### Utility Skills Not Yet Implemented

| Skill | Purpose |
|-------|---------|
| `content-repurposer` | Transform content between formats |
| `headline-generator` | Generate multiple headline options |
| `cta-optimizer` | Improve calls to action |
| `content-auditor` | Audit content against voice DNA |

---

*This guide is part of the AI Co-Writing System documentation suite.*
