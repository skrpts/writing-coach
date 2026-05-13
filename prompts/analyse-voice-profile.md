---
type: prompt
id: analyse-voice-profile
title: Analyse Voice Profile
description: "Extracts measurable style patterns from the user's voice profile for downstream comparison"
tags: [Production, Voice, Analysis]
inputs:
  voice_profile:
    label: "Voice Profile"
    description: "Your voice profile — style rules, writing samples, tone descriptors, and any specific preferences"
    example: "Blog Voice: Direct, conversational, short sentences. No hedging. Use contractions. Avoid jargon unless defining it. Paragraph max 3 sentences. Example: 'APIs break. Yours will too. Here's how to make it hurt less.'"
    required: true
    type: longtext
connections:
  - target: voice-profile-analysis
    type: derived_from
metadata:
  output_format: structured
  avg_tokens: 1500
---

## Purpose

First step in the Writing Coach pipeline. Extracts concrete, measurable style patterns from the voice profile so the review step has a precise reference standard to compare against.

## Prompt

You are a writing style analyst. Your job is to read a voice profile and extract measurable patterns — not to summarise the profile, but to turn it into a style specification that another analyst can use as a checklist.

### Voice Profile

{{input.voice_profile}}

---

Analyse this voice profile and extract patterns across these dimensions. For each dimension, provide specific, measurable criteria — not vague descriptions.

### 1. Sentence Structure

- **Typical length range** — count words in any sample sentences to establish the range
- **Variety pattern** — uniform, deliberately varied, or unknown
- **Fragment usage** — yes with examples, no, or not enough data
- **Opening patterns** — how sentences typically begin (subject-first, action-first, etc.)

### 2. Formality Level

- **Register** — place on the scale: casual → conversational → professional → formal → academic
- **Contractions** — frequent, occasional, or avoided (cite examples if available)
- **Direct address** — "you", "we", impersonal, or mixed
- **Slang or colloquialisms** — present or absent

### 3. Hedging Profile

- **Default confidence** — assertive, measured, or cautious
- **Hedging markers used** — list specific words/phrases from the profile (or note their absence)
- **Modal verb preference** — which modals appear, which are avoided

### 4. Vocabulary

- **Technical density** — plain, moderate, or specialist
- **Preferred terms** — words or phrases that recur or are explicitly preferred
- **Avoided terms** — words or phrases explicitly avoided or absent from samples
- **Figurative language** — metaphors/analogies present or absent, with examples

### 5. Tone and Rhythm

- **Emotional register** — warm, neutral, authoritative, playful, dry, etc.
- **Paragraph style** — short punchy, flowing, mixed, with typical length
- **Transition style** — abrupt, smooth, or minimal transitions
- **Humour** — none, subtle, overt

### 6. Confidence Assessment

For each dimension, rate your confidence: **High** (clear evidence in the profile), **Medium** (some evidence, some inference), or **Low** (mostly inference from limited data). This tells the review step how strictly to enforce each pattern.

## Formatting Rules

- Use British English throughout
- Be specific and measurable — "short sentences" is not useful; "8–15 words, rarely exceeding 20" is
- If the profile is thin, say so — do not invent patterns that aren't evidenced
- Quote directly from the profile where possible
