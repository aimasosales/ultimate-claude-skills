# Contributing Guidelines

**Version**: 1.0.0
**Last Updated**: 2025-01-01

---

## Table of Contents

1. [Welcome](#1-welcome)
2. [How to Contribute](#2-how-to-contribute)
3. [Contribution Types](#3-contribution-types)
4. [Development Guidelines](#4-development-guidelines)
5. [Skill Development Standards](#5-skill-development-standards)
6. [Context Profile Standards](#6-context-profile-standards)
7. [Documentation Standards](#7-documentation-standards)
8. [Testing Requirements](#8-testing-requirements)
9. [Code of Conduct](#9-code-of-conduct)

---

## 1. Welcome

Thank you for your interest in contributing to the AI Co-Writing System! This document provides guidelines for contributing to the project, whether you're adding new skills, improving documentation, or enhancing existing features.

### 1.1 Project Philosophy

This project is built on several core principles:

- **Context Engineering over Prompt Engineering**: Persistent, structured context beats one-off prompts
- **Modularity**: Each skill is self-contained and independently usable
- **User Ownership**: Users own their data and can customize everything
- **Progressive Disclosure**: Load only what's needed when it's needed
- **No Lock-in**: Standard formats (JSON, Markdown) ensure portability

### 1.2 What We're Looking For

We welcome contributions in these areas:

| Priority | Contribution Type |
|----------|-------------------|
| High | New content generation skills |
| High | Bug fixes and improvements |
| Medium | Documentation improvements |
| Medium | Context profile enhancements |
| Low | Experimental features |

---

## 2. How to Contribute

### 2.1 Quick Start

```
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit pull request
```

### 2.2 Detailed Process

#### Step 1: Fork and Clone

```bash
# Fork via GitHub UI, then:
git clone https://github.com/YOUR-USERNAME/my-writing-system.git
cd my-writing-system
```

#### Step 2: Create Branch

```bash
# Use descriptive branch names
git checkout -b feature/new-skill-name
git checkout -b fix/skill-trigger-issue
git checkout -b docs/update-user-manual
```

#### Step 3: Make Changes

Follow the guidelines in this document for your contribution type.

#### Step 4: Test

```
# Open project in Cursor
# Test with Claude Code
# Verify skills trigger correctly
# Check context profiles load
# Confirm documentation accuracy
```

#### Step 5: Commit

```bash
# Use conventional commit messages
git commit -m "feat(skills): add newsletter-writer skill"
git commit -m "fix(linkedin-post): correct character count"
git commit -m "docs: update troubleshooting guide"
```

#### Step 6: Submit PR

```bash
git push origin feature/new-skill-name
# Create pull request via GitHub
```

### 2.3 Commit Message Format

Use conventional commits:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

**Types**:
- `feat` - New feature or skill
- `fix` - Bug fix
- `docs` - Documentation only
- `style` - Formatting, no code change
- `refactor` - Code restructuring
- `test` - Adding tests
- `chore` - Maintenance tasks

**Examples**:
```
feat(skills): add youtube-script skill

Adds comprehensive YouTube script writing skill with:
- Hook framework
- Retention strategies
- CTA optimization

Closes #42
```

```
fix(voice-dna): correct JSON schema validation

The tone_sliders array was not properly validated.
Added min/max constraints for slider values.
```

---

## 3. Contribution Types

### 3.1 New Skills

Adding new skills is the most impactful contribution.

**Before starting**:
1. Check if skill already exists
2. Check if planned in CHANGELOG.md
3. Open issue to discuss skill idea

**Requirements**:
- Follow SKILL.md specification exactly
- Include multiple frameworks
- Provide concrete examples
- Reference context profiles
- Include quality checklist

See [Section 5](#5-skill-development-standards) for detailed standards.

### 3.2 Skill Improvements

Enhance existing skills:

- Add new frameworks
- Improve instructions clarity
- Add more examples
- Fix trigger issues
- Optimize output quality

### 3.3 Context Profile Enhancements

Improve context profile schemas:

- Add useful fields
- Improve field descriptions
- Add validation rules
- Enhance examples

### 3.4 Documentation

Documentation contributions:

- Fix errors or typos
- Add missing information
- Improve clarity
- Add examples
- Update outdated content

### 3.5 Bug Fixes

Fix issues with:

- Skill invocation
- Context loading
- Output formatting
- JSON validation
- File path handling

---

## 4. Development Guidelines

### 4.1 File Organization

```
my-writing-system/
├── .claude/
│   └── skills/
│       └── skill-name/
│           └── SKILL.md      # One file per skill minimum
├── context/
│   ├── voice-dna.json
│   ├── icp.json
│   └── business-profile.json
├── knowledge/
│   ├── drafts/
│   ├── notes/
│   └── archive/
├── docs/
│   └── *.md                  # Documentation files
└── claude.md                 # System instructions
```

### 4.2 Naming Conventions

#### Skills
- Lowercase only
- Hyphens between words
- Max 64 characters
- Descriptive names

```
# Good
linkedin-post
voice-dna-creator
sales-email-sequence

# Bad
LinkedIn_Post
voiceDNACreator
ses
```

#### Files
- Lowercase with hyphens for skills
- UPPERCASE.md for documentation
- lowercase.json for data files

```
# Good
SKILL.md
voice-dna.json
CONTRIBUTING.md

# Bad
skill.MD
VoiceDNA.json
contributing.MD
```

### 4.3 Code Style

#### JSON Files
- 2-space indentation
- Double quotes only
- No trailing commas
- Descriptive keys

```json
{
  "field_name": "value",
  "nested_object": {
    "inner_field": "value"
  },
  "array_field": [
    "item1",
    "item2"
  ]
}
```

#### Markdown Files
- ATX-style headers (#)
- Blank line before/after headers
- Fenced code blocks with language
- Tables aligned with pipes

```markdown
# Header 1

Content here.

## Header 2

More content.

### Code Example

```javascript
const example = "code";
```

| Column 1 | Column 2 |
|----------|----------|
| Data     | Data     |
```

---

## 5. Skill Development Standards

### 5.1 Required Structure

Every skill MUST have:

```yaml
---
name: skill-name
description: Clear description. When to use triggers.
---

# Skill Title

## When to Use This Skill
[Explicit trigger conditions]

## Before Writing
[Context loading instructions]

## Instructions
[Step-by-step process]

## Frameworks
[At least one framework with template]

## Output Format
[Expected structure]

## Examples
[At least one concrete example]

## Quality Checklist
[Validation items]
```

### 5.2 Description Requirements

The description is critical for skill discovery:

| Requirement | Example |
|-------------|---------|
| What it does | "Create engaging LinkedIn posts" |
| When to use | "Use when writing LinkedIn content" |
| Max length | 1024 characters |

**Template**:
```yaml
description: [What it does in one sentence]. Use when [trigger condition 1], [trigger condition 2], or [trigger condition 3].
```

### 5.3 Framework Requirements

Each skill should have 2-5 frameworks:

```markdown
## Frameworks

### Framework 1: Name

**When to use**: [Condition]

**Structure**:
```
[Line 1 purpose]
[Line 2 purpose]
[Line 3 purpose]
```

**Example**:
```
[Concrete example using framework]
```
```

### 5.4 Context Integration

Skills MUST reference context profiles:

```markdown
## Before Writing

1. **Read context profiles**:
   - `/context/voice-dna.json` - Match writing voice
   - `/context/icp.json` - Target audience specifics
   - `/context/business-profile.json` - Offerings and CTAs

2. **Check knowledge base** for relevant material
```

### 5.5 Quality Checklist

Every skill needs validation criteria:

```markdown
## Quality Checklist

Before delivering:
- [ ] Matches voice DNA tone and style
- [ ] Addresses ICP problems/interests
- [ ] Follows selected framework structure
- [ ] Meets length guidelines
- [ ] Includes appropriate CTA
- [ ] Free of generic AI patterns
```

---

## 6. Context Profile Standards

### 6.1 JSON Schema Requirements

All JSON files must:

- Be valid JSON (validate at jsonlint.com)
- Use snake_case for keys
- Include descriptive field names
- Have consistent structure

### 6.2 Voice DNA Standards

Required sections:
- `identity`
- `tone`
- `personality`
- `language_patterns`
- `writing_mechanics`

### 6.3 ICP Standards

Required sections:
- `primary_icp`
- `demographics`
- `psychographics`
- `problems`
- `language`

### 6.4 Business Profile Standards

Required sections:
- `business_info`
- `offerings`
- `unique_mechanism`
- `calls_to_action`
- `content_pillars`

---

## 7. Documentation Standards

### 7.1 Document Types

| Type | Format | Purpose |
|------|--------|---------|
| Guide | Step-by-step | How to do something |
| Reference | Tables, lists | Quick lookup |
| Concept | Explanatory | Understanding |
| Tutorial | Walkthrough | Learning |

### 7.2 Required Elements

Every documentation file needs:

```markdown
# Title

**Version**: X.X.X
**Last Updated**: YYYY-MM-DD

---

## Table of Contents
[Navigation links]

---

## Content Sections
[Main content]

---

*Footer with context*
```

### 7.3 Writing Style

- Use active voice
- Be concise
- Include examples
- Use consistent terminology
- Address the reader as "you"

### 7.4 Code Examples

- Always include language identifier
- Make examples runnable
- Include expected output
- Explain non-obvious parts

```markdown
```javascript
// Calculate total with tax
const total = subtotal * (1 + taxRate);
console.log(total); // Output: 108.00
```
```

---

## 8. Testing Requirements

### 8.1 Skill Testing

Before submitting a skill:

```
Test 1: Discovery
─────────────────
Ask: "What skills are available?"
Verify: Your skill appears in list

Test 2: Explicit Trigger
─────────────────
Ask: "Use the [skill-name] skill to [task]"
Verify: Skill is invoked correctly

Test 3: Implicit Trigger
─────────────────
Ask: "[Natural request that should trigger skill]"
Verify: Skill is automatically selected

Test 4: Context Integration
─────────────────
Verify: Output reflects voice DNA
Verify: Output targets ICP
Verify: Output uses business CTAs

Test 5: Framework Usage
─────────────────
Request: Each framework specifically
Verify: Output follows framework structure

Test 6: Quality
─────────────────
Verify: All checklist items pass
Verify: No generic AI patterns
Verify: Appropriate length
```

### 8.2 Context Profile Testing

```
Test 1: JSON Validity
─────────────────
Validate at: jsonlint.com

Test 2: Field Completeness
─────────────────
Check: All required fields present
Check: No placeholder text remaining

Test 3: Integration
─────────────────
Request: Content that uses profile
Verify: Profile data reflected in output
```

### 8.3 Documentation Testing

```
Test 1: Accuracy
─────────────────
Verify: All instructions work as written
Verify: All paths and commands correct

Test 2: Completeness
─────────────────
Check: All features documented
Check: All edge cases covered

Test 3: Clarity
─────────────────
Have someone unfamiliar follow docs
Note any confusion points
```

---

## 9. Code of Conduct

### 9.1 Our Standards

We are committed to providing a welcoming environment:

**Expected behavior**:
- Use inclusive language
- Be respectful of differing viewpoints
- Accept constructive criticism gracefully
- Focus on what's best for the community
- Show empathy towards others

**Unacceptable behavior**:
- Harassment or discrimination
- Trolling or insulting comments
- Personal or political attacks
- Publishing others' private information
- Other unprofessional conduct

### 9.2 Enforcement

Violations may result in:
1. Warning
2. Temporary ban
3. Permanent ban

### 9.3 Reporting

Report issues to project maintainers via:
- GitHub issues (public)
- Direct message (private)

---

## Appendix A: PR Checklist

Before submitting your PR:

```
[ ] PREPARATION
    [ ] Forked and cloned repository
    [ ] Created descriptive branch name
    [ ] Made atomic, focused changes

[ ] SKILLS (if applicable)
    [ ] SKILL.md follows specification
    [ ] Frontmatter is valid YAML
    [ ] Description under 1024 chars
    [ ] Includes trigger conditions
    [ ] References context profiles
    [ ] Has 2+ frameworks
    [ ] Has concrete examples
    [ ] Has quality checklist
    [ ] Tested all trigger methods
    [ ] Tested all frameworks

[ ] CONTEXT PROFILES (if applicable)
    [ ] Valid JSON
    [ ] All required sections present
    [ ] No placeholder text
    [ ] Tested with content generation

[ ] DOCUMENTATION (if applicable)
    [ ] Follows documentation standards
    [ ] Includes version and date
    [ ] Has table of contents
    [ ] All links work
    [ ] All commands tested
    [ ] Spell-checked

[ ] GENERAL
    [ ] Commit messages follow convention
    [ ] No unrelated changes
    [ ] Updated CHANGELOG.md
    [ ] Updated relevant docs
    [ ] All tests pass
```

---

## Appendix B: Skill Ideas

Looking for something to contribute? Consider these skills:

### High Priority
| Skill | Description |
|-------|-------------|
| newsletter-writer | Full newsletter creation |
| blog-post | SEO-optimized blog posts |
| content-repurposer | Transform between formats |
| headline-generator | Multiple headline options |

### Medium Priority
| Skill | Description |
|-------|-------------|
| youtube-script | Video scripts with hooks |
| podcast-outline | Episode planning |
| case-study | Customer success stories |
| press-release | PR announcements |

### Low Priority
| Skill | Description |
|-------|-------------|
| ad-copy | Advertising copy |
| landing-page | Conversion copy |
| product-description | E-commerce copy |
| speech-writer | Presentations |

---

## Appendix C: Resources

### Official Documentation
- [ARCHITECTURE.md](ARCHITECTURE.md) - System architecture
- [SKILLS-GUIDE.md](SKILLS-GUIDE.md) - Skill development
- [CONTEXT-PROFILES-GUIDE.md](CONTEXT-PROFILES-GUIDE.md) - Profile creation
- [USER-MANUAL.md](USER-MANUAL.md) - Usage guide

### External Resources
- [Claude Code Documentation](https://code.claude.com/docs)
- [Anthropic Agent Skills](https://docs.anthropic.com/en/docs/claude-code/agent-skills)
- [JSON Validator](https://jsonlint.com)
- [Markdown Guide](https://www.markdownguide.org)

---

*Thank you for contributing to the AI Co-Writing System!*
