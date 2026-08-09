# JSON Schemas

These files use JSON Schema Draft 2020-12 and validate complete Knowledge File module wrappers, not isolated record arrays.

| Schema | Module |
|---|---|
| `source.schema.json` | `../data/sources.json` |
| `person.schema.json` | `../data/people.json` |
| `place.schema.json` | `../data/places.json` |
| `timeline.schema.json` | `../data/timeline.json` |
| `open_question.schema.json` | `../data/open_questions.json` |
| `claim.schema.json` | Reserved contract for `../data/claims.json` |
| `photo.schema.json` | Reserved contract for `../data/photos.json` |

The five active modules were validated against these schemas when this archive was produced. `claims.json` and `photos.json` remain zero-byte placeholders and cannot be parsed as JSON. Their schemas define proposed minimum contracts without assigning canonical record-ID namespaces.

Schema validation is structural. It does not establish factual accuracy or source sufficiency and does not perform cross-file checks such as orphan detection, reciprocal-link verification, count reconciliation or source-locator review.

A minimal Python validation example:

```python
import json
from jsonschema import Draft202012Validator

with open("data/people.json", encoding="utf-8") as data_file:
    data = json.load(data_file)

with open("schemas/person.schema.json", encoding="utf-8") as schema_file:
    schema = json.load(schema_file)

Draft202012Validator.check_schema(schema)
Draft202012Validator(schema).validate(data)
```
