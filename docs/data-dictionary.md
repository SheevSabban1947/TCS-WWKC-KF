# Data Dictionary

**Applies to:** Who Was Karmein Chan? Knowledge File v0.3.0  
**Documentation revision:** 9 August 2026

This document describes the model as it exists in version 0.3.0. It is descriptive, not a substitute for working JSON schemas. Optional fields are omitted from many records.

## 1. Shared top-level fields

Most non-empty modules use some of the following fields:

| Field | Meaning |
|---|---|
| `file` | Canonical filename of the module |
| `schema_version` | Version of that module's data structure |
| `updated` | Last recorded module update date in ISO format |
| `claim_model` | Example of the atomic claim wrapper used by the module |
| `metadata` | Module-level description, counts, status, or editorial notes |
| `sources` | Small embedded source list used by some early modules |

Module versions are not uniform in v0.3.0. The package version and a module's `schema_version` are separate concepts.

## 2. Atomic claim wrapper

Many factual fields use:

| Field | Type | Meaning |
|---|---|---|
| `value` | scalar or structured value | Stored content |
| `units` | string or null | Semantic type or category |
| `precision` | string | Specificity, normalization, or transcription status |
| `inference_score` | integer | Current 0–3 evidential/editorial score |
| `source_ids` | array of strings | Supporting source catalogue IDs |

The wrapper may appear directly or inside arrays and nested objects.

## 3. `data/sources.json`

### Top level

| Field | Meaning |
|---|---|
| `metadata.description` | Purpose of the source catalogue |
| `metadata.source_count` | Declared number of source records |
| `metadata.cataloguing_basis` | Explanation of how sources were selected or represented |
| `metadata.notes` | Additional catalogue notes |
| `sources` | Array of source records |

### Source record

| Field | Meaning |
|---|---|
| `source_id` | Stable source identifier |
| `record_type` | `source` |
| `title` | Catalogued source title |
| `source_type` | Newspaper, website, broadcast, book, private contact, etc. |
| `publication_date` | Date or partial date associated with the source |
| `identifiers` | Publication, archive, edition, document, ISBN, ISSN, or other identifiers |
| `access` | URL, archive route, access limitation, or retrieval note |
| `facts_supported` | Concise descriptions of relevant information |
| `availability_status` | Public, restricted, unavailable, private, or similar access status |
| `referenced_in_current_files` | Per-file reference counts |
| `review_flags` | Source-quality, privacy, conflict, or verification warnings |

Reference counts are derived metadata and should be recomputed rather than trusted after editing other modules.

## 4. `data/people.json`

### Top level

| Field | Meaning |
|---|---|
| `metadata` | Counts, previous version, change summary, certification status, identity note |
| `layers` | Definitions of core and contextual person layers |
| `controlled_vocabularies` | Allowed or recommended status and role categories |
| `pending_global_work` | Outstanding module-wide review tasks |
| `people` | Core-case person records |
| `contextual_people` | Context-only person records |

### Person record

Common fields include:

| Field | Meaning |
|---|---|
| `id` | Stable person ID |
| `record_type` | `person` |
| `display_name` | Preferred label used by the dataset |
| `names` | Full names, aliases, pseudonyms, labels, or name components |
| `roles` | Case, family, professional, social, investigative, or contextual roles |
| `birth` | Known or reported birth date, year, or place |
| `death` | Known or reported death date or year |
| `family_relationships` | Relationship labels and linked person IDs |
| `residences` | Places and time periods associated with residence |
| `education` | School, institution, year level, class, or related facts |
| `languages` | Reported languages |
| `events` | Person-level event descriptions or links |
| `possible_same_as` | Explicit unresolved identity hypotheses |
| `context_sources` | Sources retained for limited contextual purposes |
| `entity_resolution_status` | Status of an unresolved identity problem |
| `identity_status` | Identified, unidentified, placeholder, pseudonymous, etc. |
| `public_status` | Degree to which the name or role is public |
| `record_scope` | Core graph or contextual layer |
| `verification` | Locator, review, publication, and certification controls |
| `review_flags` | Human-readable warnings and restrictions |

### Verification object

| Field | Meaning |
|---|---|
| `status` | Overall review state |
| `claim_locator_status` | Whether exact locators have been attached |
| `publication_status` | Internal, held, contextual, or otherwise publishable state |
| `review_note` | Explanation of the required work or restriction |

## 5. `data/places.json`

### Place record

| Field | Meaning |
|---|---|
| `id` | Stable place ID |
| `canonical_name` | Preferred dataset label |
| `aliases` | Alternate or historical names |
| `place_type` | Property, school, road, cemetery, business, suburb, etc. |
| `location` | Nested address, suburb, state, country, coordinate, or area fields |
| `case_roles` | Reasons the place is relevant |
| `historical_facts` | Dated or contextual facts about the location |
| `privacy_level` | Publication or sensitivity classification |
| `review_flags` | Missing source, naming conflict, precision, or privacy warnings |

Place records in v0.3.0 do not consistently include `record_type`.

## 6. `data/timeline.json`

### Top level

The module contains an embedded `sources` array and a `timeline` array. The embedded source list is not a replacement for `data/sources.json`.

### Timeline record

| Field | Meaning |
|---|---|
| `id` | Stable event ID |
| `record_type` | `timeline_event` |
| `event_type` | Controlled or normalized event category |
| `title` | Short neutral title |
| `date` | Single date or partial date |
| `start_date` / `end_date` | Date range when one date is insufficient |
| `start_time` / `end_time` | Time or time interval |
| `summary` | Concise event description |
| `source_locator` | Section anchor or other locator |
| `related_person_ids` | Linked person IDs |
| `related_place_ids` | Linked place IDs |
| `review_flags` | Conflict, precision, or verification warnings |

A record may use `date` or a date range, not necessarily both. One record in v0.3.0 is an undated status statement.

## 7. `data/open_questions.json`

### Open-question record

| Field | Meaning |
|---|---|
| `id` | Stable question ID |
| `record_type` | `open_question` |
| `category` | Thematic or source-section category |
| `question` | Question text |
| `status` | Open, partially resolved, resolved, superseded, or similar state |
| `source_locator` | Origin or section locator for the question |
| `related_person_ids` | Relevant people |
| `related_place_ids` | Relevant places |
| `related_event_ids` | Relevant timeline events |
| `review_flags` | Wording, premise, privacy, or research warnings |

In version 0.3.0, all 29 questions are marked open and most graph links remain unpopulated.

## 8. `data/claims.json`

This file is empty in version 0.3.0. The intended function is to store individually addressable atomic claims, but no operative record structure has been adopted.

`schemas/claim.schema.json` now defines a reserved minimum wrapper and record contract. It is not an active production module, and no canonical claim-ID namespace is assigned in version 0.3.0.

## 9. `data/photos.json`

This file is empty in version 0.3.0. A future photograph module should distinguish at least:

- the depicted subject;
- creator or photographer where known;
- date and location;
- provenance and source ID;
- copyright and reuse status;
- publication status;
- transformations such as crop, colourization, cleanup, or AI restoration;
- privacy and dignity restrictions.

These fields are represented in the reserved contract in `schemas/photo.schema.json`, but they are not part of an active v0.3.0 data module and no canonical photo-ID namespace is assigned.

## 10. `karmein_chan_knowledge_file.toon`

The TOON file consolidates the current modules into a compact text form. Its header contains:

- package metadata;
- input-module provenance;
- record counts;
- reference-integrity summaries;
- normalization notes.

It is optimized for ingestion rather than editing. The JSON modules remain authoritative.

## 11. Schemas

The `schemas/` directory contains seven Draft 2020-12 schemas. Five describe active module wrappers and records:

| Schema | Data module | Status |
|---|---|---|
| `source.schema.json` | `data/sources.json` | Active |
| `person.schema.json` | `data/people.json` | Active |
| `place.schema.json` | `data/places.json` | Active |
| `timeline.schema.json` | `data/timeline.json` | Active |
| `open_question.schema.json` | `data/open_questions.json` | Active |
| `claim.schema.json` | `data/claims.json` | Reserved contract; data file is zero-byte |
| `photo.schema.json` | `data/photos.json` | Reserved contract; data file is zero-byte |

The active schemas validate wrapper structure, required fields, types, record-type constants, inference-score range and identifier syntax. JSON Schema alone does not enforce cross-file referential integrity, reciprocal graph links, uniqueness across different modules, declared-count accuracy, source relevance or factual correctness.
