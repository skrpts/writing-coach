---
type: skill
id: feedback-synthesis
title: Feedback Synthesis
description: "Converts style review findings into actionable coaching feedback — specific suggestions, alternative phrasings, and an overall style consistency score"
tags: [Production, Voice, Coaching]
connections:
  - target: llm-service
    type: runs_on
metadata:
  complexity: medium
  avg_tokens: 2500
---

## Capability

Takes the passage-level style review and transforms it into coaching feedback the user can act on. For each finding, provides a specific suggestion — not "make this less formal" but "replace 'utilise' with 'use' to match your typical vocabulary".

## Feedback Components

### Inline Suggestions

For each style drift finding:

- **Location** — the specific passage or sentence
- **Issue** — what doesn't match the profile (e.g. "this sentence hedges with 'it might be possible' — your blog voice states things directly")
- **Suggestion** — a concrete alternative phrasing that matches the profile
- **Severity** — how far the passage drifts from the profile (minor, moderate, significant)

### Style Score

An overall consistency score across dimensions:

- **Tone consistency** — how well the overall tone matches the profile
- **Sentence patterns** — how well sentence structure matches
- **Vocabulary alignment** — how well word choices match
- **Hedging alignment** — how well the confidence level matches
- **Overall score** — weighted average across dimensions

### Coaching Notes

High-level observations about patterns in the drift:

- Recurring issues (e.g. "you consistently hedge in your opening paragraphs but not elsewhere")
- Strengths (e.g. "your sentence rhythm is spot-on throughout")
- Priority suggestion (the single change that would most improve consistency)

## Output Format

Returns structured coaching feedback with inline suggestions, a dimensional style score, and coaching notes. The feedback is phrased as coaching ("your blog voice is more direct here — try…") not as correction ("this is wrong").

## Limitations

The coach suggests, the user decides. Not every drift is unintentional — sometimes you want to sound different for a specific audience or context. The coach identifies drift, not errors.
