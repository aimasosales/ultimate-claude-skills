# Context Profiles Guide

**Version**: 1.0.0
**Last Updated**: 2025-01-01

---

## Table of Contents

1. [Understanding Context Profiles](#1-understanding-context-profiles)
2. [Voice DNA Profile](#2-voice-dna-profile)
3. [ICP Profile](#3-icp-profile)
4. [Business Profile](#4-business-profile)
5. [Creating Profiles](#5-creating-profiles)
6. [Maintaining Profiles](#6-maintaining-profiles)
7. [Advanced Profile Techniques](#7-advanced-profile-techniques)

---

## 1. Understanding Context Profiles

### 1.1 What Are Context Profiles?

Context profiles are **structured JSON files** that give Claude deep knowledge about:
- **Who you are** (Voice DNA)
- **Who you write for** (ICP)
- **What you do** (Business Profile)

They transform Claude from a generic AI into a personalized co-writer.

### 1.2 Why JSON Format?

| Benefit | Description |
|---------|-------------|
| **Structured** | Clear hierarchy for complex information |
| **Parseable** | AI can extract specific sections efficiently |
| **Editable** | Human-readable and modifiable |
| **Versionable** | Easy to track changes in git |
| **Extensible** | Can add new fields without breaking format |

### 1.3 Profile Location

```
my-writing-system/
└── context/
    ├── voice-dna.json         # Your voice and personality
    ├── icp.json               # Your ideal client
    └── business-profile.json  # Your business context
```

### 1.4 How Profiles Are Used

```
User Request: "Write a LinkedIn post about AI tools"
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                    CLAUDE READS:                             │
├─────────────────────────────────────────────────────────────┤
│ 1. voice-dna.json                                           │
│    → Captures your tone, phrases, personality               │
│    → Ensures output sounds like YOU                         │
│                                                             │
│ 2. icp.json                                                 │
│    → Understands your audience's problems                   │
│    → Uses language they relate to                          │
│    → Addresses their specific pain points                  │
│                                                             │
│ 3. business-profile.json                                    │
│    → References your offerings when relevant               │
│    → Maintains positioning consistency                     │
│    → Includes appropriate CTAs                             │
└─────────────────────────────────────────────────────────────┘
                           │
                           ▼
              Personalized, Targeted Content
```

---

## 2. Voice DNA Profile

### 2.1 Purpose

The Voice DNA captures your **unique writing voice, tone, and personality**. It's the most important profile because it makes AI output sound like YOU, not generic AI.

### 2.2 Complete Schema

```json
{
  "voice_dna": {
    "version": "1.0",
    "last_updated": "YYYY-MM-DD",

    "core_essence": {
      "identity": "Who you are at your core",
      "primary_role": "Your main role/function",
      "unique_angle": "What makes your perspective unique"
    },

    "personality_traits": {
      "primary": ["trait1", "trait2", "trait3"],
      "how_it_shows": {
        "trait1": "How this trait appears in writing",
        "trait2": "How this trait appears in writing"
      }
    },

    "emotional_palette": {
      "dominant_emotions": ["emotion1", "emotion2"],
      "emotional_range": {
        "excitement": "When/how you show excitement",
        "frustration": "When/how you express frustration",
        "empathy": "How you connect emotionally"
      },
      "energy_level": "Description of your energy"
    },

    "communication_style": {
      "formality": "Casual/Professional/Mixed",
      "complexity": "Simple/Complex/Varies",
      "sentence_structure": {
        "preferred_length": "Short/Medium/Long/Mixed",
        "patterns": ["pattern1", "pattern2"]
      },
      "paragraph_style": "Description of paragraph habits"
    },

    "language_patterns": {
      "signature_phrases": ["phrase1", "phrase2"],
      "power_words": ["word1", "word2", "word3"],
      "words_to_avoid": ["word - reason"],
      "transitions": ["transition1", "transition2"]
    },

    "never_say": {
      "phrases": ["phrase - reason"],
      "tones": ["tone - reason"],
      "approaches": ["approach - reason"]
    },

    "formatting_preferences": {
      "uses_emojis": true/false,
      "emoji_style": "When/how if true",
      "uses_lists": true/false,
      "list_style": "When/how",
      "uses_headers": true/false,
      "header_style": "Style description",
      "uses_bold": true/false,
      "bold_for": "What you bold"
    },

    "content_philosophy": {
      "core_belief": "What drives your content",
      "value_delivery": "How you provide value",
      "relationship_with_reader": "How you relate to readers"
    },

    "voice_examples": {
      "opening_lines": ["example1", "example2"],
      "closing_lines": ["example1", "example2"],
      "transitional_phrases": ["example1", "example2"]
    }
  }
}
```

### 2.3 Section-by-Section Guide

#### Core Essence
The fundamental "who you are" that colors everything you write.

```json
"core_essence": {
  "identity": "A founder who figured things out the hard way and shares what works",
  "primary_role": "Educator and practitioner, not guru",
  "unique_angle": "Practical AI implementation without the hype"
}
```

#### Personality Traits
The characteristics that come through in your writing.

```json
"personality_traits": {
  "primary": ["Direct", "Curious", "Slightly irreverent"],
  "how_it_shows": {
    "Direct": "Short sentences, clear points, no hedging",
    "Curious": "Asking questions, exploring ideas openly",
    "Slightly irreverent": "Challenging conventional wisdom, casual humor"
  }
}
```

#### Emotional Palette
The emotions you express and how you express them.

```json
"emotional_palette": {
  "dominant_emotions": ["Genuine enthusiasm", "Mild frustration at bad advice"],
  "emotional_range": {
    "excitement": "When sharing something that works, uses 'this is wild' type phrases",
    "frustration": "When calling out BS, direct but not mean",
    "empathy": "Acknowledges struggles without being preachy"
  },
  "energy_level": "High energy but grounded, not manic"
}
```

#### Communication Style
The mechanics of how you write.

```json
"communication_style": {
  "formality": "Conversational professional - would say it in a meeting but not in an email to the CEO",
  "complexity": "Simple language for complex ideas, no jargon unless audience knows it",
  "sentence_structure": {
    "preferred_length": "Mix of short punchy and medium explanatory",
    "patterns": ["Short. Short. Then longer explanation.", "Question? Answer."]
  },
  "paragraph_style": "Short paragraphs, 1-3 sentences, lots of white space"
}
```

#### Language Patterns
The specific words and phrases you use (and avoid).

```json
"language_patterns": {
  "signature_phrases": [
    "Here's the thing",
    "This is what actually works",
    "Let me show you"
  ],
  "power_words": ["actually", "exactly", "specifically", "wild", "game-changer"],
  "words_to_avoid": [
    "synergy - corporate speak",
    "leverage - overused",
    "guru - hate the term"
  ],
  "transitions": ["But here's the thing", "Now", "So", "Look"]
}
```

#### Never Say
Critical for avoiding generic AI output.

```json
"never_say": {
  "phrases": [
    "In today's fast-paced world - cliché opener",
    "It's no secret that - filler",
    "At the end of the day - overused"
  ],
  "tones": [
    "Preachy or condescending - we're peers",
    "Overly formal - too stiff",
    "Fake enthusiasm - readers can tell"
  ],
  "approaches": [
    "Clickbait without substance",
    "Humble bragging",
    "Vague advice without examples"
  ]
}
```

### 2.4 Voice DNA Best Practices

| Do | Don't |
|----|-------|
| Focus on TONE over word lists | Just list frequently used words |
| Include what NOT to say | Only include positives |
| Be specific with examples | Be vague about style |
| Update as your voice evolves | Set and forget |
| Test with sample content | Assume it's perfect first try |

---

## 3. ICP Profile

### 3.1 Purpose

The ICP (Ideal Client Profile) defines **who you write for**. It ensures content addresses real problems in language your audience uses.

### 3.2 Complete Schema

```json
{
  "ideal_client_profile": {
    "version": "1.0",
    "last_updated": "YYYY-MM-DD",

    "demographics": {
      "age_range": "28-45",
      "gender": "Any, slight male skew",
      "location": "US, UK, global English-speaking",
      "income_level": "$75k-250k",
      "education": "College educated"
    },

    "professional_profile": {
      "job_titles": ["Founder", "Creator", "Marketing Lead"],
      "industries": ["Tech", "Creator economy", "Professional services"],
      "company_size": "Solo to 50 employees",
      "experience_level": "3-10 years",
      "decision_making_power": "Primary decision maker"
    },

    "psychographics": {
      "values": ["Efficiency", "Authenticity", "Continuous learning"],
      "beliefs": ["AI is a tool not replacement", "Quality > quantity"],
      "personality_traits": ["Action-oriented", "Curious", "Time-conscious"]
    },

    "problems_and_pain_points": {
      "primary_problems": [
        {
          "problem": "Content takes too long to create",
          "severity": "HIGH",
          "frequency": "Daily"
        },
        {
          "problem": "AI output sounds generic",
          "severity": "HIGH",
          "frequency": "Every use"
        }
      ],
      "frustrations": [
        "Tried AI tools that produced garbage",
        "Tired of generic prompts that don't work"
      ],
      "fears": [
        "Falling behind competitors using AI",
        "Losing authentic voice to AI"
      ]
    },

    "goals_and_desires": {
      "immediate_goals": [
        "Create more content in less time",
        "Maintain voice consistency"
      ],
      "long_term_aspirations": [
        "Build content system that scales",
        "Become known thought leader"
      ],
      "dream_outcome": "Content machine that sounds authentically like them"
    },

    "language_patterns": {
      "words_they_use": ["scale", "system", "workflow", "authentic"],
      "phrases_they_say": [
        "I don't have time for this",
        "It needs to sound like me",
        "What's actually working?"
      ],
      "questions_they_ask": [
        "How do I make AI sound less generic?",
        "What's the most efficient way to do this?"
      ],
      "jargon_they_know": ["ICP", "CTR", "engagement", "funnel"]
    },

    "content_consumption": {
      "platforms": ["LinkedIn", "Twitter", "Substack"],
      "content_formats": ["Short posts", "Newsletters", "How-to threads"],
      "consumption_time": "Morning and evening",
      "attention_span": "Quick value, can go deep if earned"
    },

    "objections": {
      "common_objections": [
        {
          "objection": "I've tried AI and it doesn't work",
          "response": "You were using prompts, not systems"
        },
        {
          "objection": "This seems complicated",
          "response": "Setup once, use forever"
        }
      ],
      "trust_barriers": [
        "Skeptical of 'AI expert' claims",
        "Need to see real examples"
      ]
    },

    "buying_triggers": {
      "emotional_triggers": ["Fear of falling behind", "Desire for efficiency"],
      "logical_triggers": ["Clear ROI", "Time saved calculations"],
      "timing_triggers": ["New year planning", "Launching new product"]
    }
  }
}
```

### 3.3 Section-by-Section Guide

#### Demographics
Basic factual information about your audience.

```json
"demographics": {
  "age_range": "28-45",
  "gender": "Balanced, slight male skew in tech",
  "location": "Primarily US, UK, Canada, Australia",
  "income_level": "$75,000-$250,000 annually",
  "education": "College educated, often self-taught in specialty"
}
```

#### Professional Profile
Their work context.

```json
"professional_profile": {
  "job_titles": ["Founder/CEO", "Content Creator", "Marketing Director"],
  "industries": ["SaaS", "Creator Economy", "Agency"],
  "company_size": "Solo to 50 employees",
  "experience_level": "5-15 years total, 2-5 in current role",
  "decision_making_power": "Final decision maker or strong influencer"
}
```

#### Problems and Pain Points
**Most important section** - this drives your content.

```json
"problems_and_pain_points": {
  "primary_problems": [
    {
      "problem": "Creating consistent content takes too much time",
      "severity": "HIGH",
      "frequency": "Daily struggle"
    },
    {
      "problem": "AI output doesn't match their voice",
      "severity": "HIGH",
      "frequency": "Every time they try AI"
    },
    {
      "problem": "No system for content - everything is ad hoc",
      "severity": "MEDIUM",
      "frequency": "Weekly frustration"
    }
  ],
  "frustrations": [
    "Tried ChatGPT/Claude and got generic output",
    "Spent money on courses that were too basic",
    "Feel like they're behind on AI"
  ],
  "fears": [
    "Competitors will use AI better and outpace them",
    "Will lose their authentic voice to AI",
    "AI will make their skills obsolete"
  ]
}
```

#### Language Patterns
**Use their words** in your content.

```json
"language_patterns": {
  "words_they_use": [
    "scale", "automate", "system", "workflow",
    "authentic", "genuine", "sounds like me"
  ],
  "phrases_they_say": [
    "I don't have time to write everything myself",
    "It needs to sound like me, not AI",
    "What's actually working right now?",
    "Show me, don't just tell me"
  ],
  "questions_they_ask": [
    "How do I make AI output less generic?",
    "What tools are you using?",
    "How long did it take to set up?",
    "Can I see examples?"
  ],
  "jargon_they_know": [
    "ICP", "CTA", "engagement rate", "funnel",
    "lead magnet", "conversion", "SEO"
  ]
}
```

### 3.4 ICP Best Practices

| Do | Don't |
|----|-------|
| Be specific ("SaaS founders") | Be generic ("business owners") |
| Include actual phrases they use | Make up language |
| Document real problems | Assume problems |
| Update based on feedback | Set and forget |
| Create multiple ICPs if needed | Force one ICP to fit all |

---

## 4. Business Profile

### 4.1 Purpose

The Business Profile provides context about **what you offer**, your positioning, and how you want to be represented.

### 4.2 Complete Schema

```json
{
  "business_profile": {
    "version": "1.0",
    "last_updated": "YYYY-MM-DD",

    "company_overview": {
      "name": "Company/Brand Name",
      "tagline": "One-line description",
      "mission": "Why you exist",
      "vision": "Where you're heading"
    },

    "value_proposition": {
      "primary_value": "The #1 result you deliver",
      "unique_mechanism": "How you uniquely deliver it",
      "key_differentiators": ["Diff 1", "Diff 2", "Diff 3"]
    },

    "offerings": {
      "products": [
        {
          "name": "Product Name",
          "type": "Course/Software/etc",
          "description": "Brief description",
          "price_point": "$X or range",
          "ideal_for": "Who it's best for"
        }
      ],
      "services": [
        {
          "name": "Service Name",
          "type": "Consulting/Done-for-you/etc",
          "description": "Brief description",
          "price_point": "$X or range",
          "ideal_for": "Who it's best for"
        }
      ],
      "free_resources": [
        {
          "name": "Resource Name",
          "type": "Newsletter/Lead magnet/etc",
          "description": "Brief description",
          "value": "What people get"
        }
      ]
    },

    "positioning": {
      "market_position": "Premium/Accessible/Budget",
      "competitor_comparison": "How you differ without naming names",
      "category": "What category you compete in",
      "niche_focus": "Specific area of focus"
    },

    "brand_voice_summary": {
      "personality": "How the brand comes across",
      "tone": "Overall feeling",
      "values_demonstrated": ["Value 1", "Value 2"]
    },

    "social_proof": {
      "key_metrics": ["10,000 subscribers", "500 clients"],
      "testimonial_themes": ["Common praise 1", "Common praise 2"],
      "notable_clients_or_features": ["Feature 1", "Client 1"]
    },

    "content_pillars": {
      "primary_topics": ["Topic 1", "Topic 2", "Topic 3"],
      "content_mission": "Purpose of your content",
      "content_style": "Style/approach"
    },

    "calls_to_action": {
      "primary_cta": {
        "action": "Subscribe to newsletter",
        "url": "https://...",
        "when_to_use": "End of most content"
      },
      "secondary_ctas": [
        {
          "action": "Book a call",
          "when_to_use": "High-intent content"
        }
      ]
    },

    "platforms": {
      "primary_platform": "LinkedIn",
      "secondary_platforms": ["Twitter", "Substack"],
      "website": "https://...",
      "handles": {
        "twitter": "@handle",
        "linkedin": "URL"
      }
    }
  }
}
```

### 4.3 Business Profile Best Practices

| Do | Don't |
|----|-------|
| Keep offerings updated | Let it get stale |
| Include specific CTAs | Leave CTAs vague |
| Document actual metrics | Inflate numbers |
| Align with voice DNA | Create conflicting brand voice |

---

## 5. Creating Profiles

### 5.1 Using Creator Skills

The easiest way to create profiles:

```
# Voice DNA (requires writing samples)
"Help me create my voice DNA profile"
→ Provide 3-10 writing samples
→ Answer analysis questions
→ Review output

# ICP
"Help me create my ICP"
→ Answer interview questions
→ Be specific about your audience
→ Review output

# Business Profile
"Help me create my business profile"
→ Answer interview questions
→ Include current offerings
→ Review output
```

### 5.2 Manual Creation

If creating manually:

1. Copy the template from `/context/`
2. Replace ALL CAPS placeholders
3. Be specific and detailed
4. Test with sample content request

### 5.3 Creation Checklist

- [ ] Voice DNA: All sections completed
- [ ] Voice DNA: "Never say" section filled out
- [ ] Voice DNA: Examples included
- [ ] ICP: Problems are specific and real
- [ ] ICP: Language patterns use actual phrases
- [ ] ICP: Objections documented
- [ ] Business: Offerings are current
- [ ] Business: CTAs are actionable
- [ ] All: Version and date updated

---

## 6. Maintaining Profiles

### 6.1 Update Schedule

| Profile | Update Frequency | Trigger Events |
|---------|-----------------|----------------|
| Voice DNA | Quarterly | Style evolution, feedback |
| ICP | Quarterly | New audience insights |
| Business | Monthly | New offerings, pricing changes |

### 6.2 Update Process

1. **Review current profile** against recent content
2. **Identify gaps** or outdated information
3. **Update sections** that need changes
4. **Increment version** number
5. **Update date** field
6. **Test** with content generation

### 6.3 Version History

Consider maintaining changelog in profile:

```json
{
  "voice_dna": {
    "version": "1.2",
    "last_updated": "2025-03-15",
    "changelog": [
      "1.2 (2025-03-15): Added new signature phrases",
      "1.1 (2025-02-01): Refined emotional palette",
      "1.0 (2025-01-01): Initial creation"
    ]
  }
}
```

---

## 7. Advanced Profile Techniques

### 7.1 Multiple ICPs

If you serve different audiences:

```
context/
├── icp-founders.json
├── icp-creators.json
└── icp-marketers.json
```

Update `claude.md` to reference all:
```markdown
## Context Profiles
- voice-dna.json - My voice (always read)
- icp-founders.json - For founder-focused content
- icp-creators.json - For creator-focused content
- icp-marketers.json - For marketer-focused content
```

### 7.2 Client Profiles

For agencies/ghostwriters managing multiple voices:

```
context/
├── voice-dna-client-a.json
├── voice-dna-client-b.json
├── icp-client-a.json
└── icp-client-b.json
```

### 7.3 Product-Specific Profiles

For different product lines:

```
context/
├── product-profile-course.json
├── product-profile-saas.json
└── product-profile-service.json
```

### 7.4 Contextual Overrides

For content that needs different voice:

```json
{
  "voice_dna_override": {
    "use_case": "Formal announcements",
    "overrides": {
      "communication_style": {
        "formality": "More professional than usual"
      },
      "never_say": {
        "phrases": []  // Allow phrases normally avoided
      }
    }
  }
}
```

---

## Appendix: Profile Templates

### Minimal Voice DNA Template

```json
{
  "voice_dna": {
    "version": "1.0",
    "core_essence": {
      "identity": "",
      "unique_angle": ""
    },
    "personality_traits": {
      "primary": []
    },
    "communication_style": {
      "formality": "",
      "sentence_structure": {
        "preferred_length": ""
      }
    },
    "language_patterns": {
      "signature_phrases": [],
      "words_to_avoid": []
    },
    "never_say": {
      "phrases": [],
      "tones": []
    }
  }
}
```

### Minimal ICP Template

```json
{
  "ideal_client_profile": {
    "version": "1.0",
    "demographics": {
      "age_range": "",
      "location": ""
    },
    "professional_profile": {
      "job_titles": [],
      "industries": []
    },
    "problems_and_pain_points": {
      "primary_problems": [],
      "frustrations": []
    },
    "language_patterns": {
      "words_they_use": [],
      "questions_they_ask": []
    }
  }
}
```

---

*This guide is part of the AI Co-Writing System documentation suite.*
