# Troubleshooting Guide

**Version**: 1.0.0
**Last Updated**: 2025-01-01

---

## Table of Contents

1. [Quick Diagnostics](#1-quick-diagnostics)
2. [Setup Issues](#2-setup-issues)
3. [Skill Issues](#3-skill-issues)
4. [Context Profile Issues](#4-context-profile-issues)
5. [Output Quality Issues](#5-output-quality-issues)
6. [Performance Issues](#6-performance-issues)
7. [Common Error Messages](#7-common-error-messages)
8. [Getting Help](#8-getting-help)

---

## 1. Quick Diagnostics

### 1.1 System Health Check

Run these commands to diagnose issues:

```
# Check Claude Code connection
"Hello, are you working?"

# Verify skills are loaded
"What skills are available?"

# Check context profiles
"What do you know about my voice and audience?"

# Test file access
"Can you read /context/voice-dna.json?"
```

### 1.2 Common Quick Fixes

| Symptom | Quick Fix |
|---------|-----------|
| Claude not responding | Restart Cursor |
| Skills not found | Check folder structure |
| Wrong voice | Verify voice-dna.json is populated |
| Generic output | Ensure context profiles aren't templates |
| File not found | Check file path spelling |

---

## 2. Setup Issues

### 2.1 Claude Code Won't Connect

**Symptoms:**
- No response from Claude
- "Connection failed" errors
- Extension not loading

**Solutions:**

```
Step 1: Check Extension
─────────────────
- Open Extensions (Ctrl+Shift+X)
- Search "Claude Code"
- Ensure it's installed and enabled
- If issues, uninstall and reinstall

Step 2: Verify Authentication
─────────────────
- Command Palette → "Claude Code: Sign Out"
- Command Palette → "Claude Code: Sign In"
- Complete authentication flow

Step 3: Check Internet Connection
─────────────────
- Test internet access
- Try api.anthropic.com in browser

Step 4: Restart Cursor
─────────────────
- Close completely
- Reopen and try again
```

### 2.2 claude.md Not Loading

**Symptoms:**
- Claude doesn't know it's a co-writer
- System instructions not applied
- No awareness of skills

**Solutions:**

```
Step 1: Verify File Location
─────────────────
claude.md must be at PROJECT ROOT:
✓ my-writing-system/claude.md
✗ my-writing-system/.claude/claude.md

Step 2: Check File Name
─────────────────
Must be exactly "claude.md" (lowercase)
✗ Claude.md
✗ CLAUDE.md
✗ claude.MD

Step 3: Verify Contents
─────────────────
- Open claude.md in editor
- Ensure it has valid markdown content
- Check for syntax errors

Step 4: Start New Chat
─────────────────
- Close current Claude chat
- Open new chat (claude.md reloads)
```

### 2.3 Folder Not Recognized as Project

**Symptoms:**
- Claude can't access files
- "File not found" for existing files
- Skills not discovered

**Solutions:**

```
Step 1: Open Correctly
─────────────────
Use File → Open Folder, not File → Open File
Must open "my-writing-system" folder, not a file within it

Step 2: Check Working Directory
─────────────────
In Claude Code: "What is your current working directory?"
Should show path to my-writing-system

Step 3: Reopen Project
─────────────────
- Close Cursor
- Reopen Cursor
- File → Open Folder → my-writing-system
```

---

## 3. Skill Issues

### 3.1 Skill Not Found

**Symptoms:**
- "I don't have that skill"
- Skill not in available list
- Claude doesn't invoke expected skill

**Solutions:**

```
Step 1: Verify Folder Structure
─────────────────
Expected:
.claude/skills/skill-name/SKILL.md

Check:
- .claude folder exists (hidden folder)
- skills subfolder exists
- Each skill has its own folder
- SKILL.md file inside each folder

Step 2: Check SKILL.md Format
─────────────────
Must have YAML frontmatter:

---
name: skill-name
description: Description here
---

# Content below

Common errors:
- Missing opening ---
- Missing closing ---
- name or description missing
- Invalid YAML syntax

Step 3: Verify Name Format
─────────────────
Skill name must be:
- Lowercase only
- Hyphens for spaces (no underscores)
- Max 64 characters
- No special characters

✓ linkedin-post
✓ voice-dna-creator
✗ LinkedIn_Post
✗ voice.dna.creator
```

### 3.2 Skill Not Triggering

**Symptoms:**
- Claude doesn't use skill when expected
- Generic response instead of skill-based
- Has to be explicitly told to use skill

**Solutions:**

```
Step 1: Check Description
─────────────────
Description must include:
- WHAT the skill does
- WHEN to use it

Poor:
description: Helps with writing

Better:
description: Create engaging LinkedIn posts. Use when
writing LinkedIn content or repurposing for LinkedIn.

Step 2: Use Trigger Words
─────────────────
Include words users would say:
- "LinkedIn post" → linkedin-post
- "Twitter thread" → twitter-thread
- "email sequence" → sales-email-sequence

Step 3: Check for Conflicts
─────────────────
If two skills have similar descriptions,
Claude may choose wrong one.
Differentiate descriptions clearly.

Step 4: Explicit Invocation Test
─────────────────
"Use the linkedin-post skill to write about AI"
If this works but automatic doesn't,
description needs improvement.
```

### 3.3 Skill Output Wrong

**Symptoms:**
- Output doesn't match skill frameworks
- Missing expected sections
- Wrong structure

**Solutions:**

```
Step 1: Verify Skill Content
─────────────────
Open SKILL.md and check:
- Instructions are clear
- Frameworks are well-defined
- Examples are present

Step 2: Check Instructions Section
─────────────────
Does skill tell Claude to:
- Read context profiles?
- Follow specific frameworks?
- Structure output in specific way?

Step 3: Add Output Format Section
─────────────────
Add explicit section:

## Output Format
[Exact structure expected]

Step 4: Test with Simple Request
─────────────────
"Following the linkedin-post skill exactly,
write a post about AI tools"
```

---

## 4. Context Profile Issues

### 4.1 Profile Not Found

**Symptoms:**
- "I don't have access to your voice profile"
- Claude asks for information in profile
- Generic output despite having profiles

**Solutions:**

```
Step 1: Verify Location
─────────────────
Files must be in /context/ folder:
my-writing-system/context/voice-dna.json
my-writing-system/context/icp.json
my-writing-system/context/business-profile.json

Step 2: Check File Names
─────────────────
Must match exactly:
✓ voice-dna.json
✗ voicedna.json
✗ voice_dna.json
✗ voice-dna.JSON

Step 3: Verify JSON Validity
─────────────────
Common JSON errors:
- Trailing commas (last item before })
- Missing quotes on strings
- Single quotes instead of double
- Unescaped special characters

Use JSON validator:
https://jsonlint.com

Step 4: Test File Access
─────────────────
"Read /context/voice-dna.json"
If error, check path and permissions
```

### 4.2 Profile Not Being Used

**Symptoms:**
- Output doesn't match voice
- Generic rather than personalized
- ICP not reflected in content

**Solutions:**

```
Step 1: Check Profile Content
─────────────────
Profiles may still have template placeholders:
- "YOUR NAME HERE"
- "PLACEHOLDER"
- All caps text

Replace ALL placeholders with real content

Step 2: Verify Skills Reference Profiles
─────────────────
Check SKILL.md files include:

## Before Writing
1. Read /context/voice-dna.json
2. Read /context/icp.json

Step 3: Verify claude.md References
─────────────────
Check claude.md includes profile locations
and instructions to read them

Step 4: Explicit Request
─────────────────
"Read my voice DNA first, then write
a LinkedIn post about AI"
```

### 4.3 Invalid JSON Format

**Symptoms:**
- "Error parsing JSON"
- Profile won't load
- Partial data loaded

**Solutions:**

```
Step 1: Validate JSON
─────────────────
Copy JSON content to: https://jsonlint.com
Fix any reported errors

Step 2: Common JSON Fixes
─────────────────

Error: Trailing comma
{"items": ["one", "two",]}  ← wrong
{"items": ["one", "two"]}   ← correct

Error: Single quotes
{'name': 'value'}  ← wrong
{"name": "value"}  ← correct

Error: Unquoted keys
{name: "value"}    ← wrong
{"name": "value"}  ← correct

Error: Line breaks in strings
{"text": "line 1
line 2"}           ← wrong
{"text": "line 1\\nline 2"}  ← correct

Step 3: Recreate If Necessary
─────────────────
"Help me recreate my voice DNA profile"
Let Claude generate valid JSON
```

---

## 5. Output Quality Issues

### 5.1 Output Sounds Generic

**Symptoms:**
- Content sounds like anyone could have written it
- No personality or unique voice
- Standard AI-sounding phrases

**Solutions:**

```
Step 1: Check Voice DNA
─────────────────
Is voice-dna.json:
- Fully populated (no placeholders)?
- Specific enough?
- Including "never_say" section?

Step 2: Strengthen Voice DNA
─────────────────
Add more specific elements:
- Signature phrases you actually use
- Specific words to avoid
- Examples of your openings/closings

Step 3: Test Voice Match
─────────────────
"Review this output against my voice DNA.
Does it match? What should change?"

Step 4: Request Voice Focus
─────────────────
"Write this in a way that clearly matches
my voice DNA. Reference specific elements
from my voice profile."
```

### 5.2 Wrong Audience Targeting

**Symptoms:**
- Content too technical or too basic
- Wrong problems addressed
- Language doesn't resonate

**Solutions:**

```
Step 1: Check ICP
─────────────────
Is icp.json:
- Specific about audience?
- Including real problems?
- Using actual language patterns?

Step 2: Update ICP Language
─────────────────
Add to language_patterns:
- Actual phrases your audience uses
- Questions they ask
- Jargon they know

Step 3: Reference ICP Explicitly
─────────────────
"Write this specifically for my ICP.
Address their main problem of [X]
using language they'd use."
```

### 5.3 Content Too Long/Short

**Symptoms:**
- LinkedIn posts are 5000 characters
- Threads have 30 tweets
- Output doesn't match platform

**Solutions:**

```
Step 1: Specify Length
─────────────────
"Write a LinkedIn post under 1500 characters"
"Create a thread with exactly 10 tweets"

Step 2: Check Skill Guidelines
─────────────────
Skills should have length guidelines.
If missing, add to SKILL.md:

## Length Guidelines
- Ideal: X characters
- Maximum: Y characters

Step 3: Request Edit
─────────────────
"This is too long. Cut it to 1200 characters
while keeping the main points."
```

### 5.4 Missing CTA or Wrong CTA

**Symptoms:**
- No call to action
- CTA doesn't match business profile
- Generic CTA

**Solutions:**

```
Step 1: Check Business Profile
─────────────────
Is calls_to_action section populated?
{
  "primary_cta": {
    "action": "Subscribe to newsletter",
    "url": "https://...",
    "when_to_use": "Most content"
  }
}

Step 2: Specify in Request
─────────────────
"End with my primary CTA from business profile"
"Use my newsletter signup CTA"

Step 3: Update Skills
─────────────────
Add to skill instructions:
"Reference business profile for appropriate CTA"
```

---

## 6. Performance Issues

### 6.1 Slow Response Times

**Symptoms:**
- Long delays before response
- Timeouts
- Partial responses

**Solutions:**

```
Step 1: Check Context Size
─────────────────
Large files = slower processing
- Split large knowledge files
- Don't load unnecessary context

Step 2: Be More Specific
─────────────────
"Read the introduction from /knowledge/draft.md"
Not: "Read everything in knowledge folder"

Step 3: Network Issues
─────────────────
- Check internet stability
- Try different network
- Wait and retry

Step 4: Rate Limits
─────────────────
If using subscription, may hit rate limits.
Wait a few minutes and retry.
```

### 6.2 Context Window Issues

**Symptoms:**
- Claude "forgets" earlier conversation
- Inconsistent references
- Truncated output

**Solutions:**

```
Step 1: Start Fresh
─────────────────
Long conversations fill context window.
Start new chat for new tasks.

Step 2: Summarize and Continue
─────────────────
"Summarize what we've done so far"
Copy summary, start new chat, paste summary

Step 3: Reduce Profile Size
─────────────────
If profiles are very large:
- Remove unnecessary detail
- Split into multiple profiles
- Load only relevant profiles
```

---

## 7. Common Error Messages

### 7.1 Error Reference Table

| Error | Cause | Solution |
|-------|-------|----------|
| "File not found" | Wrong path | Check spelling, use forward slashes |
| "Invalid JSON" | Malformed JSON | Validate at jsonlint.com |
| "Skill not found" | Wrong location/format | Check .claude/skills structure |
| "Permission denied" | File locked | Close file in other apps |
| "Context too long" | Too much loaded | Start fresh, be specific |
| "Rate limited" | Too many requests | Wait and retry |

### 7.2 File Path Issues

```
WRONG:
- \context\voice-dna.json (backslashes)
- context/voice-dna.json (missing leading /)
- /Context/Voice-DNA.json (wrong case)

CORRECT:
- /context/voice-dna.json
```

### 7.3 JSON Syntax Errors

```
WRONG:
{
  "items": [1, 2, 3,]  // trailing comma
}

{
  'name': 'value'  // single quotes
}

{
  name: "value"  // unquoted key
}

CORRECT:
{
  "items": [1, 2, 3]
}

{
  "name": "value"
}
```

---

## 8. Getting Help

### 8.1 Self-Help Resources

1. **Documentation**: Review files in /docs/
2. **Skill Files**: Each SKILL.md has usage instructions
3. **Templates**: Check /context/ for format examples

### 8.2 Diagnostic Commands

```
# System info
"Describe your current setup and available skills"

# Profile check
"Summarize my voice DNA, ICP, and business profile"

# Skill check
"List all skills and their triggers"

# File system check
"List all files in the context folder"
```

### 8.3 Reporting Issues

When reporting issues, include:
1. What you tried (exact command)
2. What happened (error or wrong output)
3. What you expected
4. Context profile status (populated/template)
5. Skill status (found/not found)

### 8.4 External Resources

- Claude Code Docs: https://code.claude.com/docs
- Cursor Help: https://cursor.sh/docs
- Anthropic Support: https://support.anthropic.com

---

## Appendix: Diagnostic Checklist

Use this checklist when troubleshooting:

```
[ ] SETUP
    [ ] Cursor installed
    [ ] Claude Code extension enabled
    [ ] Authenticated with Claude
    [ ] Project folder opened (not single file)
    [ ] claude.md at project root

[ ] FILES
    [ ] .claude/skills/ folder exists
    [ ] Each skill has SKILL.md
    [ ] /context/ folder exists
    [ ] All three JSON profiles present
    [ ] JSON files are valid

[ ] PROFILES
    [ ] voice-dna.json populated (no placeholders)
    [ ] icp.json populated
    [ ] business-profile.json populated

[ ] SKILLS
    [ ] YAML frontmatter valid
    [ ] name field present (lowercase-with-hyphens)
    [ ] description field present
    [ ] Skill instructions reference context
```

---

*This guide is part of the AI Co-Writing System documentation suite.*
