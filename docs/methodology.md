# Methodology

**Applies to:** Who Was Karmein Chan? Knowledge File v0.3.0  
**Documentation revision:** 9 August 2026

## 1. Purpose

The Knowledge File is designed to preserve structured, attributable research concerning Karmein Chan, her life and context, her disappearance and murder, the investigation, and the public record that followed.

The project has four methodological goals:

1. preserve information without flattening uncertainty;
2. separate source description, supported fact, editorial normalization, inference, and speculation;
3. make relationships between people, places, events, questions, and sources inspectable;
4. support correction and further research without presenting the dataset as an official investigative record.

The project is person-centred rather than offender-centred. It seeks to document Karmein Chan as a person while treating the crime and investigation with evidential restraint.

## 2. Scope

The dataset may include:

- biographical facts about Karmein Chan;
- family, school, social, geographic, and historical context;
- events before, during, and after 13 April 1991;
- discovery, investigative, media, and memorial events;
- named public officials, investigators, specialists, witnesses, and contextual figures;
- unidentified or pseudonymous entities when the public record requires them;
- places directly connected to the case or retained for clearly labelled context;
- source metadata and access information;
- unresolved research questions.

The dataset does not claim to reproduce the complete police brief, coronial record, family archive, school archive, or every media report. Absence from the Knowledge File does not imply irrelevance or non-existence.

## 3. Source collection

Each source is assigned a stable source ID and catalogued in `data/sources.json`. A source record should identify, where available:

- title;
- source type;
- publication or creation date;
- publisher, publication, author, programme, archive, or collection identifiers;
- access locator or access note;
- a concise description of the facts for which the source is relevant;
- availability and disclosure status;
- review flags.

Sources may include newspapers, books, broadcasts, official statements, public websites, photographs, maps, archival databases, cemetery material, interviews, private correspondence, or user-generated material. Their evidential value is not assumed to be equal.

### 3.1 Source preference

Where sources conflict or vary in quality, the preferred order is generally:

1. contemporaneous primary or official records;
2. identifiable first-person testimony or direct interviews;
3. reputable contemporaneous reporting;
4. later reporting that cites identifiable evidence;
5. specialist secondary analysis;
6. public websites, compilations, and user-generated material;
7. unattributed recollection, private contact, or AI-generated material.

This is a guide rather than an automatic ranking. A later source may correct an earlier error, and an official statement may itself be provisional. The specific claim, locator, context, and known conflicts must be evaluated.

### 3.2 Private and non-disclosable sources

A source may be catalogued while its identifying details remain private. Such a source must be marked accordingly and should not become the sole public basis for a serious allegation, identification, or disputed claim.

Privacy restrictions must be preserved in derived datasets. A non-disclosable source must not be reverse-engineered from metadata or contextual clues.

## 4. Claim representation

Most factual data is stored in an atomic wrapper:

```json
{
  "value": "...",
  "units": "...",
  "precision": "...",
  "inference_score": 0,
  "source_ids": ["..."]
}
```

### 4.1 `value`

The content being asserted or recorded. It may be a name, label, date, time, address, role, status, quotation summary, identifier, or other scalar value.

### 4.2 `units`

The semantic type of the value, such as `personal_name`, `iso8601_date`, `case_role`, or `source_type`. It is not limited to physical units.

### 4.3 `precision`

The degree or manner of specificity. Examples include `day`, `year`, `suburb`, `street_address`, `controlled_label`, `paraphrased_from_timeline_entry`, or `catalogued_title`.

Precision does not measure truth. It explains how exactly the value is expressed.

### 4.4 `inference_score`

Version 0.3.0 JSON modules currently use numeric scores defined in `people.json`:

- `0`: directly asserted or exact structural reference;
- `1`: editorial normalization or unresolved entity distinction;
- `2`: explicit hypothesis that must not be stated as established fact;
- `3`: highly speculative and prohibited from publication without exceptional corroboration.

The file `docs/inference-levels.md` describes a proposed IL-0 to IL-4 framework. That proposal is not the operative field model for v0.3.0. Consumers must not silently translate between the two systems.

### 4.5 `source_ids`

An array of source IDs supporting or explaining the value. An empty array may indicate an editorial, structural, verification, or publication-control value rather than an externally sourced factual claim.

A source reference is not sufficient by itself for factual certification. Exact claim locators remain required.

## 5. Exact source locators

A material claim should be traceable to a precise location within its source. Suitable locators include:

- page and column;
- article section or paragraph;
- quotation and surrounding context;
- broadcast timestamp;
- archival image or frame number;
- document section, clause, or table;
- stable HTML anchor;
- photograph filename and region description;
- database record number.

Broad source-level references are retained during research, but records without exact locators must remain marked as pending review. Version 0.3.0 is not factually certified because this work is incomplete, especially in `people.json`.

## 6. Extraction and normalization

The project distinguishes between transcription and normalization.

- A transcription preserves source wording as closely as practical.
- A normalization converts wording into a consistent data form without adding new factual content.
- A paraphrase summarizes source meaning and must be labelled through `precision` or a review note.
- An inference goes beyond explicit wording and must receive a higher inference score.

Examples of normalization include converting a date to ISO 8601, assigning a controlled event category, using a stable display name, or representing a relationship with a person ID.

Editorial normalization must not erase ambiguity, conflict, offensive historical wording relevant to source interpretation, or distinctions between similarly described people.

## 7. Dates and times

Dates should use ISO 8601-compatible strings where possible:

- day precision: `1991-04-13`;
- month precision: `1991-04`;
- year precision: `1991`.

A date range uses separate `start_date` and `end_date` fields. Times use `start_time` and, where appropriate, `end_time`.

Estimated, inferred, approximate, or source-conflicted dates and times must be identified through `precision`, `inference_score`, `review_flags`, or an explanatory summary. A normalized timestamp must not imply greater certainty than the source provides.

## 8. People and entity resolution

Each person or person-like entity receives a stable person ID. The dataset may retain separate records for:

- a named individual;
- an unidentified person described in a source;
- a pseudonymous offender label;
- a synthetic placeholder required to preserve a relationship or account;
- a contextual person who is not part of the core case graph.

Separate entities must not be merged merely because a theory proposes that they are the same person. Possible identity relationships are recorded as unresolved hypotheses and must preserve their evidential qualification.

Synthetic ordinal labels do not establish birth order, chronology, identity, or uniqueness. They are placeholders, not factual claims.

No person should be described as a suspect, offender, accomplice, or person of interest unless the wording is supported by an exact source and accompanied by any necessary qualification. Inclusion in the file never implies guilt.

## 9. Core and contextual people

`people.json` separates:

- `people`: the core case graph;
- `contextual_people`: people retained for comparison or background but excluded from the core graph.

Contextual inclusion must not be converted into a suspect association. The `record_scope`, `verification`, and `review_flags` fields govern use.

## 10. Places and privacy

Places are recorded at the most useful precision supported by the source. A place may contain country, state, suburb, street, address, coordinates, aliases, historical facts, and case roles.

Historical addresses that are already public may still be privacy-sensitive. The presence of a public address in an old newspaper does not automatically justify repeated publication in every derivative dataset. `privacy_level` and `review_flags` must be preserved.

Current private residences, precise coordinates, or identifying details should be omitted or generalized unless a strong historical or research need exists and publication is lawful and proportionate.

## 11. Timeline construction

Timeline entries record events or status statements with stable event IDs. Each entry should include:

- an event category;
- a neutral title;
- a date, date range, or explicit undated status;
- optional times;
- a concise summary;
- source references and a locator;
- related people and places;
- review flags where needed.

A timeline entry is not automatically an independently verified event merely because it has been normalized into a chronology. Conflicting accounts should remain visible, and the conflict should be described rather than resolved by silent selection.

## 12. Open questions

Open questions are research prompts, not claims. They identify missing knowledge, unresolved conflicts, or potentially useful lines of inquiry.

An open question should:

- be neutrally worded;
- avoid embedding an unsupported premise;
- link to relevant people, places, or events where possible;
- retain its source context;
- change status only when evidence permits a documented answer.

A question may remain in the file after partial resolution if the unresolved portion is clearly restated.

## 13. Conflicting evidence

When sources conflict:

1. preserve each materially different account;
2. identify the source and exact locator for each;
3. describe the conflict neutrally;
4. assess whether the difference concerns fact, wording, date, time, identity, or interpretation;
5. avoid creating a false synthesis;
6. prefer a conclusion only when the evidential basis is stated.

A later editorial choice must not erase the existence of the earlier conflict.

## 14. Review flags and verification status

Review flags are operative warnings, not decorative comments. They may require the user to:

- verify exact wording;
- avoid merging identities;
- avoid inferring guilt;
- restrict publication;
- confirm a place or date;
- resolve a source conflict;
- add a missing source ID or locator.

In `people.json`, the verification object records:

- review status;
- locator status;
- publication status;
- a review note.

Derived exports must preserve these controls. A clean-looking export that drops holds or warnings is methodologically defective.

## 15. Publication decisions

Before a record is approved for public presentation, the editor should confirm:

- identity and spelling;
- exact source support;
- an exact locator for each material claim;
- neutral and proportionate wording;
- correct inference score;
- correct record scope;
- privacy and legal considerations;
- consistency with connected records;
- absence of an unresolved publication hold.

Sensitive allegations require a higher threshold than ordinary biographical or chronological facts.

## 16. JSON and TOON workflow

The JSON modules are the editable source of truth. The TOON file is a derived compact representation for language-model ingestion.

A correct export process should:

1. parse all non-empty JSON modules;
2. validate IDs and references;
3. preserve claim wrappers, review flags, and publication controls;
4. recompute record and reference counts;
5. write provenance metadata from the current module headers;
6. compare the TOON output against the JSON source;
7. report missing or unused references without silently repairing the source files.

Version 0.3.0 does not yet include the reproducible generation and validation tooling required to guarantee this process.

## 17. Quality-control checklist

A release review should check:

- every non-placeholder JSON file parses;
- schema and module versions are coherent;
- IDs are unique and conform to their namespace;
- all cross-referenced IDs exist;
- no retired ID has been reused;
- source counts and module counts are accurate;
- exact locators exist for publishable material claims;
- review flags and holds are preserved;
- privacy-sensitive fields have been reviewed;
- source conflicts are explicit;
- the TOON provenance matches the JSON headers;
- the README and citation identify the correct version and date.

## 18. Corrections and versioning

Corrections should be additive and auditable where practical. A correction should identify the affected record, previous value, replacement value, supporting source and locator, reason, editor, and release version.

IDs should remain stable across corrections. A record should be deprecated rather than silently replaced when its identity or conceptual meaning changes substantially.

The project uses semantic-style versioning as described in the README.

## 19. Known limitations of version 0.3.0

- Exact source locators are incomplete.
- The people module is explicitly uncertified pending locator review.
- Many people records are internal-only or held.
- Two modules are empty placeholders.
- Schemas do not yet validate the actual model.
- The operative inference-score model and the proposed IL model differ.
- Some catalogued sources are not yet connected to records.
- Some people are not yet connected to the wider graph.
- The TOON provenance contains known module-version inconsistencies.
- The dataset remains heavily dependent on the project website as an intermediate source for timeline entries and open questions.

These limitations do not make the dataset unusable, but they constrain the claims that can responsibly be made from it.
