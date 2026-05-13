---
type: skill
id: text-style-review
title: Text Style Review
description: "Compares input text against extracted voice profile patterns — identifies specific passages where the writing drifts from the user's established style"
tags: [Production, Voice, Review]
connections:
  - target: llm-service
    type: runs_on
metadata:
  complexity: high
  avg_tokens: 2000
---

## Capability

Takes the extracted style patterns from the voice profile analysis and compares them against the user's input text. Identifies specific passages, sentences, and word choices where the text diverges from the user's established voice.

This is not a grammar checker or a readability scorer. It is a style consistency detector — it answers "does this sound like me?" with evidence.

## Review Dimensions

### Tone Drift

- Passages where the formality level shifts away from the profile
- Sections that feel warmer, colder, or more distant than the user's typical voice
- Inconsistencies within the text itself (tone shifts mid-document)

### Sentence Pattern Mismatches

- Sentences significantly longer or shorter than the profile's established range
- Missing variety where the profile favours variation, or unexpected variation where the profile is uniform
- Fragment usage (or absence) that contradicts the profile

### Hedging Detection

- Hedging language ("it might be possible", "arguably", "one could say") in a voice that is typically direct
- Overly assertive statements in a voice that favours measured qualification
- Modal verb usage that doesn't match the profile's confidence level

### Vocabulary Drift

- Technical terms where the profile favours plain language (or vice versa)
- Formal words replacing casual equivalents the profile prefers
- Missing signature phrases or patterns the profile typically uses

### Structural Patterns

- Paragraph lengths that don't match the profile's rhythm
- Missing or unexpected transitions
- List usage where the profile favours prose (or vice versa)

## Output Format

Returns a passage-level review: each finding identifies a specific location in the text, the style dimension it violates, the expected pattern (from the profile), and what was found instead. Findings are sorted by severity (high drift first).

## Limitations

Style is subjective. The review identifies divergence from the profile, not objective quality issues. A passage might "drift" from the profile intentionally — the user decides whether to accept or dismiss each finding.
