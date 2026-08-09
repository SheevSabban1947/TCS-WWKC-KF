# Who Was Karmein Chan? Knowledge File

**Dataset version:** 0.3.0  
**Dataset date:** 6 August 2026  
**Documentation revision:** 9 August 2026  
**Project:** [The Cruel Song — Who Was Karmein Chan?](https://thecruelsong.com/)

The **Who Was Karmein Chan? Knowledge File** is a structured, source-driven research dataset concerning Karmein Chan: her life, family and social context, her abduction and murder, the subsequent investigation, and her public memory.

Its purpose is to:

- preserve attributable information in a reusable form;
- distinguish documented facts from inference, uncertainty and open questions;
- connect people, places, events and sources through stable identifiers;
- support careful human research and language-model-assisted analysis;
- remember Karmein Chan as a person, not merely as a victim in a criminal case.

This is an independent, non-profit research project. It is **not** an official Victoria Police, coronial, court, school, cemetery or family record. Inclusion of a person, place, source or question does not imply criminal responsibility, endorsement or official recognition.

## Release status

Version 0.3.0 is an **experimental pre-publication release**. It can be inspected, tested and cited, but it should not yet be described as a complete or fully certified public database.

The principal publication blockers are:

- exact page, column, paragraph, timestamp, quotation or equivalent locators are still missing from many material claims;
- many person records remain marked `internal_only_pending_review`, `hold` or `contextual_only_internal`;
- `data/claims.json` and `data/photos.json` are reserved but empty;
- the JSON schemas are placeholders and do not yet validate the real data model;
- the operative `inference_score` system and the proposed inference-level documentation are not yet fully consolidated;
- the TOON export contains known provenance-version inconsistencies and must not override the modular JSON files.

These limitations must be disclosed whenever version 0.3.0 is redistributed or described publicly.

## Dataset contents

Version 0.3.0 contains **241 catalogued records**:

| Module | Records | Purpose |
|---|---:|---|
| `data/sources.json` | 65 | Sources, provenance and access information |
| `data/people.json` | 80 | 76 core people and 4 contextual people |
| `data/places.json` | 17 | Locations connected to the case or its later context |
| `data/timeline.json` | 50 | Dated, ranged, timed and undated events |
| `data/open_questions.json` | 29 | Unresolved research questions |
| `data/claims.json` | 0 | Reserved for future atomic claims |
| `data/photos.json` | 0 | Reserved for future photograph metadata |

The total excludes metadata objects and embedded source summaries contained inside other modules.

## Package structure

```text
.
├── README.md
├── LICENSE
├── karmein_chan_knowledge_file.toon
├── data/
│   ├── claims.json
│   ├── open_questions.json
│   ├── people.json
│   ├── photos.json
│   ├── places.json
│   ├── sources.json
│   └── timeline.json
├── docs/
│   ├── data-dictionary.md
│   ├── id-system.md
│   ├── inference-levels.md
│   └── methodology.md
└── schemas/
    └── *.schema.json
```

Historical development files may also appear in `docs/`. They are retained for provenance and must not be treated as current data modules.

## Authoritative files

The modular JSON files in `data/` are the editable source of truth.

`karmein_chan_knowledge_file.toon` is a compact, single-file export intended primarily for language-model ingestion. It is derived from the JSON modules and is not independently authoritative. When JSON and TOON disagree:

1. use the JSON value;
2. record the discrepancy;
3. regenerate or correct the TOON export in a later release.

`data/claims.json` and `data/photos.json` are zero-byte placeholders in version 0.3.0. Software must check their size before attempting to parse them.

## Data model

The dataset is divided into five active entity types.

### Sources

`data/sources.json` catalogues newspapers, broadcasts, books, websites, podcasts, archival material, private communications and other evidence-bearing material.

A source record describes what the source is and how it may be accessed. A source ID does not, by itself, prove that the source supports every claim attached to it. Exact claim locators remain necessary.

### People

`data/people.json` records named, anonymous, pseudonymous and context-only individuals. Person records may contain:

- names and aliases;
- roles and relationships;
- biographical facts;
- links to events, places and sources;
- verification and publication controls;
- review flags and identity-resolution notes.

Inclusion is not an accusation. Records marked `hold`, `internal_only_pending_review` or `contextual_only_internal` are not approved for unrestricted public reuse.

### Places

`data/places.json` records residences, schools, businesses, public locations, investigative sites and other geographically relevant places.

Historical addresses may be retained for research accuracy, but publication should be proportionate and sensitive to current privacy risks.

### Timeline events

`data/timeline.json` records dated, approximate, ranged, timed and undated events. Dates and times may have different levels of precision. Consumers must preserve the associated precision and inference metadata.

### Open questions

`data/open_questions.json` records unresolved research problems. An open question is not a factual assertion. It identifies uncertainty, a missing source, a conflict or a possible line of investigation.

### Atomic values

Many factual values use an atomic claim wrapper similar to:

```json
{
  "value": "Karmein Chan",
  "units": "personal_name",
  "precision": "common_public_name",
  "inference_score": 0,
  "source_ids": ["TCS-WWKC-WEB-0001", "KCSRC00006"]
}
```

The principal fields are:

- `value`: the stored fact, label, date, statement, identifier or status;
- `units`: the semantic type or controlled category of the value;
- `precision`: how specifically or exactly the value is expressed;
- `inference_score`: the current evidential or editorial distance score;
- `source_ids`: identifiers of supporting catalogue entries.

Relationships are represented through stable IDs rather than by copying full records. See:

- `docs/data-dictionary.md` for modules and fields;
- `docs/id-system.md` for identifier rules;
- `docs/methodology.md` for sourcing, verification and editorial practice.

## Recommended reading and import order

For a first inspection, use this order:

1. `README.md`;
2. `docs/methodology.md`;
3. `docs/id-system.md`;
4. `docs/data-dictionary.md`;
5. `data/sources.json`;
6. `data/people.json` and `data/places.json`;
7. `data/timeline.json`;
8. `data/open_questions.json`;
9. `karmein_chan_knowledge_file.toon`, only when a compact single-file representation is useful.

Applications should load `sources.json` before resolving source references from the other modules.

## Usage instructions

### Manual inspection

The JSON files are UTF-8 text and can be opened in a code editor or JSON viewer. Avoid editors that silently reorder arrays, alter Unicode characters or convert numeric-looking identifiers.

### Command line with `jq`

```bash
# Show source-file metadata and count records
jq '.metadata, (.sources | length)' data/sources.json

# List person IDs and display names
jq '.people[] | {id, display_name: .display_name.value}' data/people.json

# List timeline IDs, dates and titles
jq '.timeline[] | {id, date: .date.value, title: .title.value}' data/timeline.json

# Find person records that are not approved for public use
jq '.people[] | select(.verification.publication_status.value != "public") |
    {id, name: .display_name.value, status: .verification.publication_status.value}' \
    data/people.json
```

Field paths may vary where a record intentionally uses a different structure. Consult `docs/data-dictionary.md` rather than assuming every nested object is identical.

### Python

```python
import json
from pathlib import Path

root = Path(".")

with (root / "data" / "sources.json").open(encoding="utf-8") as handle:
    sources_file = json.load(handle)

with (root / "data" / "people.json").open(encoding="utf-8") as handle:
    people_file = json.load(handle)

sources_by_id = {
    source["id"]: source
    for source in sources_file["sources"]
}

for person in people_file["people"]:
    person_id = person["id"]
    display_name = person["display_name"]["value"]
    publication_status = person["verification"]["publication_status"]["value"]
    print(person_id, display_name, publication_status)
```

Production consumers should add explicit type checks and report unresolved IDs rather than silently discarding them.

### JavaScript / Node.js

```javascript
import { readFile } from "node:fs/promises";

const peopleFile = JSON.parse(
  await readFile("data/people.json", "utf8")
);

for (const person of peopleFile.people) {
  const id = person.id;
  const name = person.display_name.value;
  const status = person.verification.publication_status.value;
  console.log({ id, name, status });
}
```

### Language-model use

For broad question answering or exploratory analysis, provide the TOON file to a model together with explicit instructions such as:

> Use the Knowledge File as a secondary research dataset. Preserve record IDs and uncertainty markers. Do not treat open questions, inferred statements or held records as established facts. Where possible, identify the underlying source IDs and state when an exact source locator is unavailable.

For high-accuracy work, provide the relevant JSON modules instead of relying only on the TOON export. A language model should never be asked to infer guilt, identify anonymous people or fill missing evidence from plausibility alone.

### Creating a derivative dataset

A derivative export should:

1. preserve canonical record IDs;
2. preserve source IDs and verification metadata;
3. exclude records whose publication status is not appropriate for the target audience;
4. retain uncertainty, precision and inference fields;
5. record the source Knowledge File version;
6. document any transformation, omission or normalisation;
7. avoid converting open questions into affirmative claims.

## Verification and publication controls

A source reference is only a pointer. Material claims should ultimately have an exact locator, such as:

- page and column;
- paragraph or section;
- broadcast timestamp;
- archive frame;
- quoted wording;
- stable document anchor;
- image region or caption.

The following fields are especially important in `people.json`:

- `verification.status`;
- `verification.claim_locator_status`;
- `verification.publication_status`;
- `verification.review_note`;
- `review_flags`;
- `record_scope`.

A record marked `hold` must not be presented as an allegation, suspect identification or established association. A record marked `internal_only_pending_review` or `contextual_only_internal` requires fresh review before inclusion in a public derivative.

## Known limitations

Version 0.3.0 has the following known limitations.

### Incomplete claim-level provenance

Many records identify relevant sources without identifying the exact passage supporting each atomic claim. This reduces independent verifiability and is the largest remaining factual-certification task.

### Uneven source quality

The source catalogue includes primary records, professional journalism, documentaries, podcasts, websites, social-media material, private communications and model-assisted estimates. These categories do not carry equal evidential weight.

### Internal and held records

A large portion of the people layer remains subject to editorial, privacy, identity or evidential review. Public derivatives must not export those records indiscriminately.

### Empty future modules

`claims.json` and `photos.json` are reserved namespaces rather than implemented modules. Their presence does not indicate that claim-level or image-level cataloguing is complete.

### Placeholder schemas

The schemas in `schemas/` currently accept broad arrays and do not enforce the actual wrappers, required fields, controlled values or reference integrity of version 0.3.0.

### Inference-model transition

The current JSON data uses numeric `inference_score` values. Documentation relating to a proposed IL-0–IL-4 framework does not yet constitute an adopted migration. Consumers must use the values actually stored in the JSON.

### TOON synchronisation

The TOON file is a derived convenience export and may contain stale module-version labels or reference-count discrepancies. It must not be used to overwrite the JSON modules.

### Incompleteness

Absence from the dataset does not establish that a person, event, place, source or theory is irrelevant or false. The Knowledge File records the current state of an ongoing research project.

### No evidentiary or legal authority

The dataset is not a police brief, sworn statement, expert report or legal finding. It should not be used as the sole basis for accusations, identification, publication of private information or contact with people connected to the case.

## Responsible use and sensitivity

This dataset concerns the abduction and murder of a child, surviving relatives, witnesses, investigators, publicly discussed suspects and people whose identities may be unknown or disputed.

Users must:

- use neutral and attributable language;
- avoid implying guilt from inclusion in the dataset;
- avoid speculative identification of anonymous or pseudonymous people;
- preserve distinctions between separate unidentified entities;
- respect non-disclosable and private source boundaries;
- avoid republishing sensitive addresses without a clear research justification;
- distinguish hypotheses and open questions from established facts;
- correct errors transparently;
- avoid harassment, vigilantism, doxxing and sensationalism.

The Knowledge File is intended to document a person and a case, not to create new harm.

## Citation

### Citing the complete release

Recommended citation:

> The Cruel Song project. *Who Was Karmein Chan? Knowledge File*. Version 0.3.0, 6 August 2026. https://thecruelsong.com/

Where the access date matters:

> The Cruel Song project. *Who Was Karmein Chan? Knowledge File*. Version 0.3.0, 6 August 2026. Accessed 9 August 2026. https://thecruelsong.com/

### Citing a record

Include the version, module and canonical record ID:

> The Cruel Song project. *Who Was Karmein Chan? Knowledge File* v0.3.0, `data/timeline.json`, record `KCEVT0021`.

Examples:

> The Cruel Song project. *Who Was Karmein Chan? Knowledge File* v0.3.0, `data/sources.json`, record `KCSRC00034`.

> The Cruel Song project. *Who Was Karmein Chan? Knowledge File* v0.3.0, `data/people.json`, record `KCPER00001`.

> The Cruel Song project. *Who Was Karmein Chan? Knowledge File* v0.3.0, `data/open_questions.json`, record `KCOQ00001`.

### Citing factual claims

The Knowledge File is a secondary research dataset. When publishing a factual claim, cite the underlying source listed in `data/sources.json` as well as, or instead of, the Knowledge File. Where no exact locator is available, state that limitation.

## Contributions and corrections

Corrections are preferred over speculative expansion. A proposed change should include:

1. the affected canonical record ID, or a clear request for a new record;
2. the exact field to add, replace or remove;
3. proposed neutral wording;
4. the relevant source ID, or full details for a new source;
5. an exact source locator;
6. an explanation of any conflict with existing records;
7. relevant privacy, identity or publication concerns;
8. the contributor's preferred attribution, if any.

Acceptable supporting material includes lawfully obtained and reviewable:

- contemporaneous newspaper pages;
- official records and public statements;
- books and academic publications;
- broadcast recordings with timestamps;
- archived webpages;
- photographs with provenance;
- clearly identified first-hand testimony, handled according to its disclosure restrictions.

The project does not accept unsupported accusations, attempts to identify anonymous people through guesswork, unlawfully obtained personal information or claims based only on repetition across derivative websites.

### Review process

A proposed contribution may be:

- accepted as documented fact;
- accepted with an inference or precision marker;
- added as an open question;
- retained internally pending review;
- rejected for insufficient evidence, duplication, privacy or safety concerns.

Canonical IDs must not be changed merely to reorder records. Corrections should preserve an auditable history in the next release notes or changelog.

## Contact

**Project website:** https://thecruelsong.com/

**Project page:** *Who Was Karmein Chan?* on The Cruel Song website.

No dedicated dataset email address or public issue tracker is included in version 0.3.0. Until one is published, correction requests and research correspondence should use the public contact route made available by The Cruel Song project. Do not send sensitive personal information through an insecure public channel.

## Release history

| Version | Date | Summary |
|---|---|---|
| 0.1.0 | 2026 | Initial single-file TOON Knowledge File. |
| 0.2.0 | 2026 | Major expansion and audit of the people layer, including unidentified actors and identity-separation rules. |
| 0.2.1 | 2026 | Patch-level people update, including Kelvin “Kel” Glare. |
| 0.3.0 | 6 August 2026 | Modular package containing 65 sources, 80 people, 17 places, 50 timeline events and 29 open questions. |

Earlier packages retained under `docs/` are development artefacts. They may not reproduce the current structure, identifiers or publication controls.

## Versioning policy

The project uses semantic-style version numbers:

- a **major** version may introduce an incompatible data model or identifier policy;
- a **minor** version may add modules, records or substantial structure;
- a **patch** version may correct records, metadata, references, exports or documentation without redesigning the model.

Documentation-only revisions do not change the dataset version unless they alter the interpretation or permitted use of stored data.

## Licence and third-party rights

The project declares the Knowledge File under the GNU General Public License version 3; see `LICENSE`.

That licence does not transfer ownership of third-party newspaper articles, photographs, broadcasts, books, archival documents, websites, trademarks or private communications described by the source catalogue. Source metadata, quotations, extracts and linked material remain subject to their original rights and applicable law.

Users are responsible for determining whether permission, licensing, quotation limits, privacy review or other legal conditions apply to their intended reuse.

## Further documentation

- `docs/methodology.md`: sourcing, verification, privacy and editorial method;
- `docs/id-system.md`: canonical identifier namespaces and assignment rules;
- `docs/data-dictionary.md`: module and field reference;
- `docs/inference-levels.md`: inference-framework documentation and transition status.
