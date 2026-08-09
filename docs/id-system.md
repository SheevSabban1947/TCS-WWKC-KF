# Identifier System

**Project:** *Who Was Karmein Chan? Knowledge File*  
**Applies to dataset version:** 0.3.0  
**Documentation revision:** 9 August 2026

## 1. Purpose

The Knowledge File uses stable, opaque identifiers to link records across modules without depending on names, descriptions, dates, or conclusions that may later change.

An identifier answers only: **which dataset record is being referenced?** It does not establish that the record is accurate, public, verified, relevant, or evidentially connected to another record.

The presence of a person ID in an event record means only that the event record refers to that person record. It does not, by itself, prove the event or imply guilt, suspicion, responsibility, or identity equivalence.

## 2. Normative language

The terms **MUST**, **MUST NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** describe requirements for editors, generators, validators, and downstream consumers.

## 3. General rules

1. Every record in an active module MUST have one canonical record ID.
2. IDs MUST be ASCII strings using the exact uppercase forms documented below.
3. IDs are case-sensitive.
4. An ID MUST be unique within its namespace.
5. A published ID MUST remain attached to the same conceptual record in later releases.
6. An ID MUST NOT change merely because a name, date, spelling, description, source, status, or interpretation changes.
7. IDs MUST NOT encode conclusions about identity, guilt, chronology, importance, or reliability.
8. Retired, merged, removed, or suppressed IDs MUST NOT be reassigned.
9. Numeric suffixes MUST retain their leading zeroes.
10. Gaps in a sequence are valid and MUST NOT be filled by recycling IDs.
11. Matching numeric suffixes in different namespaces have no meaning.
12. Cross-references MUST reproduce the canonical target ID exactly.
13. Record IDs are distinct from URLs, ISBNs, ISSNs, archive references, page numbers, or website revision labels.
14. A new namespace MUST be documented before permanent IDs are issued under it.

## 4. Active namespaces in version 0.3.0

| Record class | Pattern | Validation regular expression | Assigned records | Module |
|---|---|---|---:|---|
| Project website source | `TCS-WWKC-WEB-NNNN` | `^TCS-WWKC-WEB-[0-9]{4}$` | 1 | `data/sources.json` |
| Other source | `KCSRCNNNNN` | `^KCSRC[0-9]{5}$` | 64 | `data/sources.json` |
| Person | `TCS-WWKC-PPL-NNNN` | `^TCS-WWKC-PPL-[0-9]{4}$` | 80 | `data/people.json` |
| Place | `KCPLACENNNN` | `^KCPLACE[0-9]{4}$` | 17 | `data/places.json` |
| Timeline event | `KCEVTNNNN` | `^KCEVT[0-9]{4}$` | 50 | `data/timeline.json` |
| Open question | `KCQSTNNNN` | `^KCQST[0-9]{4}$` | 29 | `data/open_questions.json` |

`N` represents one decimal digit.

The assigned ranges in version 0.3.0 are:

- `TCS-WWKC-WEB-0001`;
- `KCSRC00001` through `KCSRC00064`;
- `TCS-WWKC-PPL-0001` through `TCS-WWKC-PPL-0080`;
- `KCPLACE0001` through `KCPLACE0017`;
- `KCEVT0001` through `KCEVT0050`;
- `KCQST0001` through `KCQST0029`.

These are current ranges, not permanent upper limits.

## 5. Record IDs and other identifier-like strings

### 5.1 Canonical record IDs

Canonical record IDs identify records inside the Knowledge File. Examples:

- `KCSRC00034` identifies a source record;
- `TCS-WWKC-PPL-0001` identifies a person record;
- `KCPLACE0001` identifies a place record;
- `KCEVT0021` identifies a timeline record;
- `KCQST0029` identifies an open-question record.

### 5.2 External identifiers

Values stored under source metadata may be ISBNs, ISSNs, archive numbers, document references, edition details, URLs, or descriptive labels. They are not Knowledge File record IDs unless they match an active namespace and occupy an ID-bearing field.

The string `TCS-WWKC-0038`, recorded as a website version visible on the source page, is **not** a record ID and MUST NOT be used as a cross-reference. The canonical source ID for the page is `TCS-WWKC-WEB-0001`.

### 5.3 IDs mentioned in prose

An ID may appear inside a note, review flag, or narrative string. Such a mention is human-readable text, not a structured cross-reference. Software SHOULD resolve only the ID-bearing fields documented in section 11 unless it deliberately parses prose.

## 6. Source IDs

### 6.1 Project website sources

Pattern: `TCS-WWKC-WEB-NNNN`

Version 0.3.0 contains one such record:

- `TCS-WWKC-WEB-0001` — *The Cruel Song – Who Was Karmein Chan?*

A change to the page title, layout, URL, or visible revision number does not automatically require a new ID. The ID SHOULD remain when the record still represents the same continuing publication. A new ID SHOULD be assigned when a materially distinct page or version must be cited and evaluated independently.

### 6.2 General sources

Pattern: `KCSRCNNNNN`

The suffix contains five digits and is assigned sequentially. A source ID identifies one catalogue entry, not every statement contained in the source.

Separate source records SHOULD be created when independent citation or assessment is required, including for:

- different newspaper articles;
- materially different editions;
- separate archival documents;
- distinct television or radio broadcasts;
- different private communications;
- substantively different versions of an online publication.

Metadata corrections, repaired links, or additional access information normally retain the existing source ID.

### 6.3 Embedded source summaries

`data/timeline.json` and `data/open_questions.json` contain local `sources` arrays. Their `source_id` values MUST correspond to canonical records in `data/sources.json`. These summaries do not create additional source records.

Many catalogue fields also include `source_ids` identifying the project source from which the catalogue description was derived. Those references do not change the record’s own `source_id`.

## 7. Person IDs

Pattern: `TCS-WWKC-PPL-NNNN`

The namespace covers both arrays in `data/people.json`:

- `people`, containing the core case graph;
- `contextual_people`, containing contextual records excluded from the core graph.

Moving a record between those arrays MUST NOT change its ID.

Version 0.3.0 contains 80 person IDs. The core array contains IDs `0001`–`0075` and `0080`; the contextual array contains `0076`–`0079`. Array position therefore MUST NOT be used to infer an ID, layer, or sequence.

A person ID may represent:

- a named individual;
- an unidentified individual distinguished by a sourced description;
- a pseudonymous person;
- a synthetic ordinal placeholder used to preserve separation between unresolved individuals;
- a contextual person retained for comparison or background.

The existence of a person record does not prove every attached description, make the person publicly identifiable, or establish involvement in an offence.

### 7.1 Identity uncertainty

When two records may represent the same person but the evidence is insufficient, both IDs MUST be retained. The uncertainty SHOULD be represented through `possible_same_as`, together with its rationale, status, sources, and inference score.

Consumers MUST NOT merge records merely because:

- names or descriptions are similar;
- both records appear in one source;
- both are associated with the same place or event;
- a `possible_same_as` relation exists;
- a public theory treats them as identical.

A possible identity is not an established identity.

### 7.2 Naming an unidentified person

If a previously unidentified record is later reliably named, the existing ID normally remains and the record is updated. A separate ID is required when the named person and placeholder remain unresolved or are shown to be distinct.

## 8. Place IDs

Pattern: `KCPLACENNNN`

A place record may represent a property, institution, road, suburb, cemetery, business premises, police facility, geographic area, or another relevant location.

Aliases, historical names, corrected spellings, and business-name changes normally remain within the same record. A new ID SHOULD be assigned when the data concerns a distinct physical or institutional entity.

Editors SHOULD distinguish between:

- an institution and one of its campuses;
- a road and an individual property on that road;
- a suburb and a location within the suburb;
- one site with several historical names and two separate nearby sites.

A changed address does not automatically create a new place ID. The decision depends on whether the record represents a continuing institution or a specific physical site.

## 9. Timeline-event IDs

Pattern: `KCEVTNNNN`

An event ID identifies one normalized timeline item. It does not certify the event as true or exact.

The same ID SHOULD be retained when wording, dates, times, sources, participants, places, or review notes are corrected while the record still represents the same conceptual occurrence.

An event SHOULD be split when its components have materially different dates, locations, participants, source support, verification status, publication restrictions, or conceptual meaning. Events MUST NOT be split merely to create precision unsupported by the sources.

Numeric event order is not an authoritative chronology. Consumers MUST sort using the event date and time fields and account for approximate, ranged, conflicting, and undated values.

## 10. Open-question IDs

Pattern: `KCQSTNNNN`

An open-question ID identifies a research problem, not a factual claim.

A question SHOULD retain its ID when wording is clarified, sources are added, related records are linked, or its status changes. If one question is divided into materially independent questions, the original SHOULD be marked appropriately and each new question MUST receive a new ID.

An answered, closed, or retired question ID MUST NOT be reused for another question.

## 11. ID-bearing fields in version 0.3.0

### 11.1 Canonical ID fields

| Module | Collection | Field | Namespace |
|---|---|---|---|
| `data/sources.json` | `sources[]` | `source_id` | source |
| `data/people.json` | `people[]` | `id` | person |
| `data/people.json` | `contextual_people[]` | `id` | person |
| `data/places.json` | `places[]` | `id` | place |
| `data/timeline.json` | `timeline[]` | `id` | event |
| `data/open_questions.json` | `open_questions[]` | `id` | question |

### 11.2 Cross-reference fields

| Field or path | Required target |
|---|---|
| any atomic claim’s `source_ids[]` | source ID |
| `context_sources[].source_id.value` | source ID |
| `family_relationships[].person_id.value` | person ID |
| `possible_same_as[].person_id.value` | person ID |
| person-event `person_id.value` fields | person ID |
| `related_person_ids[]` | person ID |
| `related_place_ids[]` | place ID |
| `related_event_ids[]` | event ID |
| embedded `sources[].source_id` | source ID |

Some references use the atomic-claim wrapper:

```json
{
  "person_id": {
    "value": "TCS-WWKC-PPL-0002",
    "units": "person_id",
    "precision": "exact_record_reference",
    "inference_score": 0,
    "source_ids": ["KCSRC00006"]
  }
}
```

`person_id.value` is the cross-reference. The neighbouring `source_ids` support the asserted relationship or identification; they do not alter the target record.

### 11.3 Directionality

Cross-references are directional at the storage level. An event may reference a person without the person record containing a reciprocal event link. Consumers MAY construct reverse indexes, but MUST NOT infer additional meaning from the presence or absence of reciprocal links.

## 12. Assigning a new ID

Editors SHOULD follow this sequence:

1. Determine the correct record class.
2. Search the relevant module for an existing record.
3. Check names, aliases, descriptions, dates, sources, unresolved identity links, and deprecated IDs.
4. Decide whether the material expands an existing record or represents a distinct entity.
5. Preserve uncertainty rather than forcing a merge.
6. Find the highest suffix already assigned in the namespace.
7. Select the next unused integer and preserve the required width.
8. Confirm that the ID has never been assigned, retired, merged, or reserved.
9. Create the record with its sources, review controls, and publication status.
10. Add cross-references only to existing canonical IDs.
11. Run syntax, uniqueness, and referential-integrity checks.
12. Record the assignment in release notes or the project change log.

Example: after `KCPLACE0017`, the next ordinary place ID is `KCPLACE0018`, not `KCPLACE18`, `kcplace0018`, or `KC-PLACE-0018`.

Sequential assignment is an editorial mechanism only. It does not indicate chronology, relevance, family order, culpability, or certainty.

## 13. Corrections and renaming

A record keeps its ID when editors change spelling, capitalization, preferred name, aliases, dates, descriptions, roles, addresses, sources, verification status, publication status, review notes, inference scores, or question wording.

Previous values SHOULD be preserved as aliases, historical values, correction notes, or change-log entries when provenance requires it.

## 14. Merging records

When two records are confirmed to represent the same conceptual entity:

1. choose one surviving canonical ID;
2. combine supported data without erasing conflicts or provenance;
3. mark the other ID as deprecated or merged;
4. record a replacement pointer when the data model supports one;
5. update active cross-references to the surviving ID;
6. preserve the retired ID in migration notes or a tombstone;
7. document the reason and supporting sources;
8. never reassign the retired ID.

Version 0.3.0 has no formal tombstone schema. Until one is added, merges SHOULD be documented in release notes and editorial history rather than performed as silent deletion.

## 15. Splitting records

When one record is found to combine distinct entities:

1. determine whether the original ID can remain with the best-supported original concept;
2. assign new IDs to the newly separated records;
3. redistribute facts and sources conservatively;
4. retain ambiguity where the evidence does not allow a clean separation;
5. update cross-references;
6. document the split and migration path.

A split MUST NOT turn uncertain information into established fact merely because it has been moved into separate records.

## 16. Retirement, removal, and suppression

An ID may be retired because its record was created in error, merged, superseded, or removed from a public edition for privacy or legal reasons. The ID remains permanently reserved.

Where lawful and safe, editorial history SHOULD retain a non-sensitive tombstone containing:

- retired ID;
- retirement status;
- date;
- reason;
- replacement ID, if any;
- release in which the change occurred.

Public suppression never authorizes ID reuse.

## 17. Inactive modules

`data/claims.json` and `data/photos.json` are zero-byte placeholders in version 0.3.0. They contain no canonical records and have no active namespaces.

No permanent claim or photograph ID pattern is defined in this release. Proposed strings such as `KCCLAIMNNNN` or `KCPHOTONNNN` MUST NOT be treated as canonical unless a later release formally adopts them in this document and in the corresponding schemas.

## 18. Validation requirements

A release validator SHOULD check:

### Syntax

- exact namespace pattern;
- uppercase and punctuation;
- suffix width;
- absence of surrounding whitespace.

### Uniqueness

- no duplicate canonical ID within a namespace;
- no person record duplicated across the two people arrays;
- no retired ID reassigned;
- no embedded source summary treated as a second canonical record.

### Referential integrity

- every `source_ids[]` value exists in `data/sources.json`;
- every person reference exists in `data/people.json`;
- every place reference exists in `data/places.json`;
- every event reference exists in `data/timeline.json`;
- every reference targets the correct namespace.

### Export integrity

- JSON and TOON preserve the same canonical IDs;
- export does not add, remove, renumber, or transform IDs;
- record counts exclude embedded source summaries;
- retired-ID migrations remain documented.

### Version 0.3.0 structural audit

At this documentation revision, the active JSON modules contain:

- no duplicate canonical IDs;
- no gaps within the currently assigned numeric ranges;
- no structured cross-reference to an absent canonical record.

This result certifies only structural consistency, not factual accuracy.

## 19. Citation and correction requests

A specific record may be cited as:

> The Cruel Song project, *Who Was Karmein Chan? Knowledge File*, v0.3.0, `data/timeline.json`, `KCEVT0021`.

The record ID locates the normalized dataset entry. It does not replace citation of the underlying source and exact locator.

A correction request SHOULD state:

- dataset version;
- module;
- canonical record ID;
- field or path;
- proposed correction;
- supporting source ID;
- exact source locator.

## 20. Downstream use

Consumers MUST preserve canonical IDs when filtering, transforming, indexing, embedding, or exporting records.

Consumers SHOULD:

- retain the dataset version beside stored IDs;
- preserve publication and review controls;
- maintain unresolved identity distinctions;
- treat missing reciprocal links as absence of stored linkage, not proof of no relationship;
- avoid creating apparent official IDs for extracted facts;
- distinguish local application keys from canonical Knowledge File IDs.

A downstream application MAY create internal keys, but those keys MUST NOT be presented as official Knowledge File identifiers.

## 21. Future changes

Adding a namespace or formalizing claim or photograph IDs requires coordinated updates to:

- this specification;
- the appropriate JSON schema;
- the data dictionary;
- validators and export tools;
- release notes;
- migration documentation where existing records are affected.

Existing canonical IDs MUST remain valid unless a documented migration corrects a structural error. A namespace redesign alone is not sufficient reason to renumber published records.
