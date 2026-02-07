# OCAM JSON Schema

Formal JSON Schema definitions for the Open Coaching Annotation Model.

## Files

| File | Description |
|------|-------------|
| `ocam-annotation.schema.json` | Main annotation schema (JSON Schema 2020-12) |

## Usage

### Validation with Node.js (ajv)

```javascript
import Ajv from "ajv/dist/2020";
import addFormats from "ajv-formats";
import schema from "./ocam-annotation.schema.json";

const ajv = new Ajv();
addFormats(ajv);
const validate = ajv.compile(schema);

const annotation = { /* your annotation */ };
if (validate(annotation)) {
  console.log("Valid OCAM annotation");
} else {
  console.log(validate.errors);
}
```

### Validation with Python (jsonschema)

```python
import json
from jsonschema import validate, Draft202012Validator

with open("ocam-annotation.schema.json") as f:
    schema = json.load(f)

annotation = { ... }  # your annotation
validate(instance=annotation, schema=schema, cls=Draft202012Validator)
```

### VS Code / IDE Integration

Add to your `.vscode/settings.json`:

```json
{
  "json.schemas": [
    {
      "fileMatch": ["examples/*.json", "annotations/*.json"],
      "url": "./schema/ocam-annotation.schema.json"
    }
  ]
}
```

## Schema Structure

### Required Fields

- `@context` - W3C Web Annotation + OCAM namespace
- `type` - Must be "Annotation"
- `sport` - Sport identifier (tennis, american-football, etc.)
- `domain` - technique | tactics | error
- `body` - Annotation content (comments, tags)
- `target` - Video/image with selectors

### Optional Fields

- `id` - Unique URN/URL identifier
- `motivation` - commenting, describing, tagging
- `created` / `modified` - ISO 8601 timestamps
- `creator` - Coach/analyst info
- `context` - Sport-specific context (stroke, phase, situation)
- `intent` - What athlete tried to do
- `outcome` - What actually happened
- `errorType` - unforced | forced (when domain is error)
- `cause` - Error cause analysis
- `sequence` - Step-by-step breakdown

### Selectors

- **FragmentSelector** - Temporal anchoring using Media Fragments (`t=start,end`)
- **SvgSelector** - Spatial annotations (SVG markup) optionally refined by temporal anchor
