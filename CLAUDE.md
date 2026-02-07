# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **Open Coaching Annotation Model (OCAM)** specification repository. It defines an open, sport-specific annotation profile for stills, videos, and streams built on the W3C Web Annotation standard.

This is a **documentation-only repository** - no code, build system, or tests. The specification enables interoperability between coaching tools across sports.

## OCAM Core Concepts

When working with this specification, understand these key design principles:

- **Sport-agnostic top level, sport-specific at lower levels** - The schema should work for any sport
- **Human and machine coaches** - Annotations must be machine-readable but human-usable
- **Stable for analytics, flexible for coaching language** - Balance consistency with expressiveness
- **Shallow hierarchies** - Don't overwhelm coaches with deep nesting
- **Separation of observation and interpretation** - What happened (error) vs why (technique)

## Core Annotation Dimensions

- **Domain**: technique / tactics / error
- **Context**: stroke, phase, situation
- **Intent**: what the athlete tried to do
- **Outcome**: what actually happened
- **Physical** (optional)
- **Mental** (optional)

## Annotation Capabilities

The specification supports:
- Temporal anchoring (timestamps, time ranges)
- Frame-accurate spatial annotations (points, lines, polygons, freehand strokes)
- Object tracking (player, racket, ball)
- Semantic labels and categories
- Narrative elements (text comments, voice notes, step-by-step sequences)
- Authorship and versioning

## Examples

See `/examples` for sample annotations demonstrating OCAM with tennis and American football:
- Technique feedback (stroke mechanics, ball handling)
- Tactical analysis (court positioning, progression reads)
- Error classification (separating observation from cause)
- Step-by-step sequences (drill breakdowns)
