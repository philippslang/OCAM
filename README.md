# Open Coaching Annotation Model (OCAM)
We define an open sport-specific annotation profile for stills, videos and streams built on top of the W3C Web Annotation standard.

- For coaches
    - Same annotations usable across tools
    - Long-term athlete development tracking
    - Share feedback between clubs, federations, analysts

- For developers
    - Clear schema
    - No lock-in
    - Easy export/import

- For federations
    - Data portability
    - Coach education consistency

## Core concepts
- Video reference
    - URI, file hash, duration, frame rate

- Temporal anchoring
    - Timestamp (t=12.34s)
    - Time ranges ([12.3s–15.8s])

- Frame-accurate anchors (optional but important for sport)
    - Spatial annotations
    - Points, lines, polygons
    - Freehand strokes
    - Object tracks (player, racket, ball)

- Semantic layer
    - Labels (“late contact”)
    - Categories (footwork, timing, tactics)
    - Tags

- Narrative / pedagogy
    - Text comments
    - Voice notes
    - Step-by-step sequences
    - Authorship & versioning
    - Coach, athlete, team
    - Revisions over time

## Design guideline
- Sport-agnostic at the top
- Sport-specific at lower levels
- Cater to human and artificial coaches
    - Machine-readable but human-usable
- Stable enough for analytics, flexible enough for coaching language
- Shallow top levels (don’t overwhelm coaches)
- Clear separation between what happened (error) and why (technique)
- Extensible to any sport
- Supports tactic and technique feedback


## Core dimensions
- Domain – technique / tactics / error
- Context – stroke, phase, situation
- Intent – what the athlete tried to do
- Outcome – what actually happened
- Physical (optional)
- Mental (optional)


## Examples
Need to cover both technical and tactical level. For tennis, this means supporting both feedback on e.g. forehand takeaway and court position. For American Football e.g. both ball handling and passing to open player.