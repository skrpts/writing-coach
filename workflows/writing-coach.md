---
type: workflow
id: writing-coach
title: Writing Coach
description: "Analyses your writing against your voice profile — identifies tone drift, hedging, formality mismatches, and sentence patterns, then provides specific coaching feedback"
tags: [Production, Voice, Coaching]
connections:
  - target: voice-profile-analysis
    type: uses
  - target: text-style-review
    type: uses
  - target: feedback-synthesis
    type: uses
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "20-40 seconds"
  avg_tokens: 6000
  trigger: manual
output_step: "feedback-synthesis"
composite_steps:
  - "voice-profile-analysis"
  - "text-style-review"
  - "feedback-synthesis"
execution:
  - skill: "voice-profile-analysis"
    prompt: "analyse-voice-profile"
    step_type: "analysis"
  - skill: "text-style-review"
    prompt: "review-text-style"
    step_type: "review"
    context:
      voice_analysis: "{{steps.Voice Profile Analysis.output}}"
  - skill: "feedback-synthesis"
    prompt: "synthesise-feedback"
    step_type: "synthesis"
    context:
      style_review: "{{steps.Text Style Review.output}}"
      voice_analysis: "{{steps.Voice Profile Analysis.output}}"
---

## Overview

The Writing Coach analyses any text against your voice profile and tells you where it drifts from your established style. Not a grammar checker — a style consistency coach that knows YOUR writing and pushes you toward sounding like yourself.

## Pipeline

### Step 1: Voice Profile Analysis

**Skill:** voice-profile-analysis | **Prompt:** analyse-voice-profile

Reads your voice profile and extracts measurable style patterns: sentence length ranges, formality level, hedging tendencies, vocabulary preferences, and tone markers. This becomes the reference standard for the review.

**Input:** Your voice profile (style rules, writing samples, tone descriptors).

**Output:** Structured style specification with confidence ratings for each dimension.

### Step 2: Text Style Review

**Skill:** text-style-review | **Prompt:** review-text-style

Compares your text against the extracted style patterns. Identifies specific passages where the writing diverges from your voice — tone shifts, hedging where you're normally direct, formal vocabulary where you prefer plain language, sentence lengths outside your typical range.

**Input:** The text to review, optional review focus.

**Output:** Passage-level findings with dimension, severity, and evidence.

### Step 3: Feedback Synthesis

**Skill:** feedback-synthesis | **Prompt:** synthesise-feedback

Transforms the review findings into coaching feedback you can act on. For each finding, provides a specific rewritten alternative that matches your voice profile. Includes a dimensional style score and coaching notes on patterns and priorities.

**Output:** Inline suggestions with rewrites, style score (1–10 per dimension), and coaching notes.

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.voice_profile}}` | Yes | Your voice profile with style rules and samples | Blog Voice: Direct, short sentences, no hedging |
| `{{input.text_to_review}}` | Yes | The text to review | Paste any text you've written |
| `{{input.review_focus}}` | No | Focus on a specific dimension | "Check for hedging" |

## Outputs

| Name | Description |
|------|-------------|
| Coaching feedback | Inline suggestions with rewrites, style score, and coaching notes |

## How It Differs from Grammar Checkers

Grammar checkers find errors against universal rules. The Writing Coach finds drift against YOUR rules — your voice, your style, your patterns. A sentence can be grammatically perfect and still "not sound like you". That's what this catches.

## Setup

No external services required beyond your configured LLM provider. Works best with a detailed voice profile — the richer your profile (with writing samples and explicit preferences), the more precise the coaching.

## Provider Notes

- Works well with any capable model — the task is comparative analysis, not creative generation
- Longer texts (2,000+ words) benefit from models with generous context limits
- The profile analysis step is lightweight; most tokens go to the text review and feedback synthesis

## Example Input

To test this workflow immediately after import, use **Try with Examples** — the pre-populated example contains a blog post draft with deliberate style inconsistencies against a direct, conversational voice profile.
