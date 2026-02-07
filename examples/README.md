# OCAM Examples

Example annotations demonstrating the Open Coaching Annotation Model (OCAM) for tennis and American football.

## Tennis Examples

| File | Domain | Description |
|------|--------|-------------|
| `tennis-technique.json` | Technique | Forehand takeaway timing feedback with spatial marker |
| `tennis-tactics.json` | Tactics | Court positioning and shot selection feedback |
| `tennis-error.json` | Error | Error analysis separating what happened from why |

## American Football Examples

| File | Domain | Description |
|------|--------|-------------|
| `football-technique.json` | Technique | QB-RB handoff ball placement |
| `football-tactics.json` | Tactics | QB progression reads and eye discipline |
| `football-sequence.json` | Technique | Step-by-step 3-step drop mechanics |

## Annotation Structure

All examples follow the W3C Web Annotation format with OCAM extensions:

```json
{
  "@context": ["http://www.w3.org/ns/anno.jsonld", { "ocam": "..." }],
  "type": "Annotation",
  "sport": "tennis | american-football",
  "domain": "technique | tactics | error",
  "context": { ... },
  "intent": "What the athlete tried to do",
  "outcome": "What actually happened",
  "body": [ ... ],
  "target": {
    "source": "video-url",
    "selector": [ temporal, spatial ]
  }
}
```

## Selector Types

- **FragmentSelector**: Temporal anchoring using Media Fragments (`t=start,end`)
- **SvgSelector**: Spatial annotations (circles, lines, paths, text) anchored to specific frames
