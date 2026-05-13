---
type: skill
id: voice-profile-analysis
title: Voice Profile Analysis
description: "Extracts measurable style patterns from a voice profile: sentence length, formality, hedging tendencies, vocabulary preferences, and tone markers"
tags: [Production, Voice, Analysis]
connections:
  - target: llm-service
    type: runs_on
metadata:
  complexity: medium
  avg_tokens: 1500
---

## Capability

Reads a voice profile and extracts concrete, measurable style patterns that the downstream review step can compare against. This is not a summary of the profile — it is a structured extraction of quantifiable style dimensions.

## Analysis Dimensions

### Sentence Structure

- **Average sentence length** — short (under 12 words), medium (12–25), long (25+)
- **Sentence variety** — does the profile favour uniform lengths or deliberate variation?
- **Fragment usage** — does the voice use intentional fragments for emphasis?

### Formality Level

- **Register** — casual, conversational, professional, formal, academic
- **Contractions** — frequent, occasional, or avoided
- **Direct address** — does the voice use "you", "we", or impersonal constructions?

### Hedging Patterns

- **Confidence markers** — does the voice state things directly or qualify with "perhaps", "it might be", "arguably"?
- **Modal verbs** — frequency of "could", "should", "might", "would"
- **Certainty level** — assertive, measured, or cautious

### Vocabulary Preferences

- **Technical density** — plain language, moderate jargon, or specialist vocabulary
- **Word choice patterns** — preferred terms, avoided terms, signature phrases
- **Figurative language** — metaphors, analogies, or strictly literal

### Tone Markers

- **Emotional register** — warm, neutral, authoritative, playful, dry
- **Humour usage** — none, subtle, frequent
- **Paragraph rhythm** — short punchy paragraphs, flowing prose, or mixed

## Output Format

Returns a structured style profile with each dimension scored and evidenced. This becomes the reference standard for the text review step.

## Limitations

The quality of pattern extraction depends on the depth of the voice profile. Thin profiles (a few sentences of description) produce coarse patterns. Rich profiles (with writing samples and explicit style rules) produce precise, actionable patterns.
