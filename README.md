# Open Coaching Annotation Model (OCAM)

We define a sport annotation profile for streams, videos and stills built on top of the W3C Web Annotation standard.

## Why
- For coaches
   - Same annotations usable across tools
   - Long-term athlete development tracking
   - Share feedback between clubs, federations, analysts
- For developers:
   - Clear schema
   - No lock-in
   - Easy export/import
- For federations:
   - Data portability
   - Coach education consistency

## V0
### Example
```json
{
  "type": "Annotation",
  "id": "anno-001",
  "role": "observation",
  "target": {
    "source": "video.mp4",
    "selector": {
      "type": "FragmentSelector",
      "value": "t=12.40"
    }
  },
  "aspect": {
    "domain": "technique"
  },
  "body": {
    "description": "Racket face opens",
    "svgSegments": [
      "<line x1='820' y1='460' x2='900' y2='420' />",
      "<line x1='820' y1='520' x2='900' y2='480' />"
    ]
  }
}
```

### Components
```
Annotation
├── id
├── role                  (observation | suggestion)
├── target                -> as in W3C Web Annotation
│   ├── source
│   └── selector          (FragmentSelector)
├── aspect
│   └── domain            (technique | tactics | physical | mental | rules)
└── body
    ├── description
    └── svgSegments       (0..n)
```

### Scope

Version 0 defines a minimal, interoperable model for annotating sport video for coaching purposes.

The scope of v0 is intentionally limited to support core coaching use cases while remaining easy to implement and aligned with existing web standards.

#### In scope

v0 supports:

1. **Temporal anchoring of annotations to video**

   * Annotations reference a video resource and are anchored in time using the W3C Media Fragments specification (`FragmentSelector`).

2. **Multiple annotations at the same time position**

   * Any number of annotations may target the same timestamp or time range.

3. **Annotation roles**

   * Each annotation declares its coaching role, such as:

     * `observation`
     * `suggestion`
   * Roles distinguish between descriptive and prescriptive coaching actions.

4. **High-level performance aspect classification**

   * Each annotation includes an `aspect` with a single `domain` field.
   * v0 defines the following domain values:

     * `technique`
     * `tactics`
     * `physical`
     * `mental`
     * `rules`
     * `other`
   * The `other` value allows for extension without breaking compatibility.

5. **Textual and visual annotation content**

   * Annotations may include:

     * Free-form description
     * One or more SVG segments representing drawings (e.g. lines, arrows, paths).
   * SVG content is treated as visual explanation, not as a spatial selector.

6. **Standards alignment**

   * v0 reuses existing standards where applicable:

     * W3C Web Annotation Data Model
     * W3C Media Fragments
     * SVG for vector-based visual content

#### Non-Goals 

Version 0 explicitly does **not** attempt to address the following:

1. **Styling or rendering rules**

   * v0 does not define colors, line styles, animation, or visual conventions.
   * Rendering decisions are left to consuming applications.

2. **Spatial selection of video regions**

   * v0 does not include spatial selectors or region-based targeting of the video frame.
   * SVG drawings are used only as explanatory visuals.

3. **Evaluation, errors, or performance judgment**

   * v0 does not model success, failure, errors, severity, or scoring.
   * No distinction is made between correct and incorrect performance.

4. **Sport-specific taxonomies**

   * v0 does not define controlled vocabularies for skills, techniques, tactics, or drills.
   * Domain values are intentionally high-level and sport-agnostic.

5. **Relationships between annotations**

   * v0 does not define formal links between annotations (e.g. “correction of”, “follows from”).
   * Each annotation stands independently.

6. **Real-time collaboration or synchronization**

   * v0 does not define protocols, APIs, or real-time communication mechanisms.

7. **User, permission, or workflow models**

   * v0 does not address authorship, roles, permissions, versioning, or review workflows.


### Design intent

The intent of v0 is to establish a small, stable foundation that:

* Reflects real coaching practice
* Encourages interoperability between tools
* Avoids premature complexity
* Allows incremental extension in future versions without breaking compatibility

Future versions may extend this model with additional semantics, controlled vocabularies, evaluation layers, and interaction models, while remaining backward compatible with v0.

### W3C
This model is a constrained profile of the W3C Web Annotation Data Model. It reuses the core Annotation, Target, and Selector concepts, including Media Fragments for temporal anchoring, while introducing domain-specific simplifications and extensions tailored to sport coaching. The profile restricts representation choices to improve implementability and interoperability, while remaining losslessly mappable to standard Web Annotations.


## Rationale

### Design goals

The primary goal of this model is to enable simple, interoperable video annotations for sport coaching that can be shared across tools, sports, and contexts.

In particular, the design prioritizes:

* Faithful representation of real coaching practice
* Low implementation complexity
* Reuse of existing, widely adopted web standards
* A clear path for future extension without breaking compatibility

### Reuse of existing standards

Rather than defining a new annotation mechanism, this model is intentionally based on the W3C Web Annotation Data Model.

Key elements are reused directly:

* The `Annotation` concept as the top-level unit
* The separation between `target` (what is annotated) and `body` (the annotation content)
* The use of Media Fragments (`FragmentSelector`) for temporal anchoring of video

By reusing these components, the model benefits from:

* Established semantics
* Existing tooling and expertise
* Long-term stability

Where the W3C model is intentionally generic, this profile introduces domain-specific constraints and simplifications to better fit coaching use cases.

### Minimal temporal anchoring

Annotations are anchored in time using Media Fragments, which are designed to identify temporal segments of audiovisual media.

Only temporal selectors are included in v0. Spatial selectors are explicitly excluded to:

* Reduce complexity
* Avoid premature decisions about coordinate systems
* Focus on the most common coaching practice: time-based feedback

This choice does not prevent future versions from adding spatial selectors if needed.

### SVG for visual annotation content

Coaches frequently use drawings (lines, arrows, shapes) to explain movement, positioning, and intent.

SVG is used for visual content because it is:

* Vector-based and resolution independent
* Expressive enough for common coaching drawings
* Widely supported and web-native

Rather than embedding full SVG documents, v0 allows SVG segment(individual elements such as `<line>` or `<path>`). This keeps annotations lightweight and easy to edit while leaving rendering decisions to consuming applications.

### Separation of role and content

Each annotation declares a `role` (e.g. `observation`, `suggestion`) that captures the intent of the coaching action.

This reflects real coaching workflows, where:

* Observations describe what happened
* Suggestions propose changes or alternatives

Separating role from content allows multiple annotations at the same timestamp to coexist without ambiguity and enables user interfaces to present or filter them differently.

### High-level aspect classification

Annotations include an `aspect` with a single `domain` field that classifies the dimension of performance being addressed.

The v0 domain values (`technique`, `tactics`, `physical`, `mental`, `rules`, `other`) are intentionally broad and sport-agnostic.

This provides:

* Immediate semantic value
* Consistent categorization across sports
* A foundation for later refinement

Detailed taxonomies and sport-specific vocabularies are deferred to future versions.

### Intentional simplicity in v0

Version 0 is deliberately minimal.

It does **not** attempt to model:

* Evaluation or errors
* Success or failure
* Styling or visual conventions
* Relationships between annotations
* User roles, permissions, or workflows

These concerns are important, but including them in v0 would increase complexity and risk premature design decisions.

Instead, v0 establishes a **stable core** that can be extended incrementally.

### Constrained profile rather than generic framework

The W3C Web Annotation model is intentionally flexible, but that flexibility can make implementations inconsistent.

This specification defines a **constrained profile** by:

* Fixing required fields
* Limiting optionality
* Restricting vocabularies where appropriate

This improves interoperability and lowers the barrier to adoption while remaining compatible with the underlying standard.

### Forward compatibility

All design choices in v0 are made with forward compatibility in mind.

Future versions may introduce:

* Spatial selectors
* Evaluation and error modeling
* Annotation relationships
* Controlled vocabularies
* Real-time collaboration

These can be added without invalidating v0 annotations or breaking existing implementations.

### Summary

This model aims to capture the **essence of coaching video annotation** with the smallest possible set of concepts.

By combining:

* Established web standards
* Minimal but meaningful semantics
* Explicit non-goals

v0 provides a practical foundation that is both usable today and extensible tomorrow.


## v1 Extension Rationale

### Purpose of v1

Version 1 is expected to build on the stable foundation established in v0 by introducing **additional semantic depth and expressive power**, while preserving backward compatibility and implementation simplicity.

The goal of v1 is **not** to fully model coaching or performance analysis, but to support richer coaching workflows that naturally emerge once basic annotation is in place.

### Extension principles

All v1 extensions should adhere to the following principles:

1. **Backward compatibility**

   * All valid v0 annotations must remain valid in v1.
   * New features must be optional and ignorable by v0 implementations.

2. **Layered complexity**

   * Extensions should be additive and orthogonal.
   * No single extension should be required for others to function.

3. **Clear separation of concerns**

   * Observation, interpretation, and prescription should remain distinguishable.
   * Visual explanation should remain separate from semantic meaning.

4. **Alignment with existing standards**

   * Where applicable, v1 should continue to reuse or align with W3C Web Annotation, Media Fragments, and related standards.

### Anticipated v1 extensions (non-exhaustive)

The following areas are identified as **likely candidates** for v1 extensions. Their inclusion is justified by common coaching practice, but their exact design is intentionally left open.

#### 1. Spatial selectors and regions of interest

**Rationale**
Coaches often want to indicate *where* in the frame an observation applies (e.g. body position, spacing, target area).

**Guidance**

* Spatial selectors should remain optional.
* They should clearly distinguish between:

  * Selecting a region of interest
  * Drawing visual explanations
* Coordinate systems must be explicitly defined.

#### 2. Aspect refinement and controlled vocabularies

**Rationale**
High-level domains are sufficient for v0, but analysis and consistency benefit from finer classification over time.

**Guidance**

* Domain values may be extended, but not replaced.
* Additional fields (e.g. skill, phase, intent) should be nested under `aspect`.
* Controlled vocabularies should be sport-agnostic at higher levels and sport-specific only where necessary.

#### 3. Evaluation and outcome modeling

**Rationale**
Coaches frequently evaluate performance, distinguish errors, and track progress.

**Guidance**

* Evaluation should be modeled as a separate concern from observation and suggestion.
* Error, success, and outcome should not be conflated with technique or tactics.
* Evaluation fields should remain optional and non-prescriptive.

#### 4. Relationships between annotations

**Rationale**
Coaching often involves connecting observations to suggestions, or grouping annotations into a narrative.

**Guidance**

* Relationships should be explicit and typed (e.g. “suggests correction for”).
* Annotations should remain independently valid.
* Relationship modeling should not imply ordering unless explicitly stated.

#### 5. Temporal refinement and frame accuracy

**Rationale**
High-speed and multi-angle sport video often requires frame-level precision.

**Guidance**

* Media Fragments should remain the primary temporal mechanism.
* Frame or fps information should extend, not replace, temporal selectors.
* Time ranges should be supported consistently.

#### 6. Multiple bodies and media types

**Rationale**
Future coaching tools may include audio notes, images, or external references.

**Guidance**

* Additional body types should follow the Web Annotation body model.
* Text and SVG should remain first-class and sufficient for basic use.

#### 7. Styling and rendering hints (non-normative)

**Rationale**
Different tools may wish to visually distinguish observations, suggestions, or emphasis.

**Guidance**

* Styling should be optional and non-normative.
* Semantic intent must not be encoded solely through visual style.
* Accessibility considerations should be respected.

### What v1 should still avoid

Even in v1, certain concerns should remain out of scope:

* Coaching methodologies or prescriptive training models
* Automated judgments or performance scoring
* Real-time synchronization protocols
* User management, permissions, or institutional workflows

These are better handled at the application or platform level.

### Evolution strategy

The model is expected to evolve incrementally:

* v0 establishes **structure and anchoring**
* v1 adds **semantics and relationships**
* Later versions may address **analysis, collaboration, and interoperability at scale**

Each version should remain usable in isolation and understandable without requiring full adoption of future features.

### Summary

By respecting the principles of backward compatibility, layered complexity, and standards alignment, contributors can extend the model in ways that support real coaching practice while preserving interoperability and long-term viability.
