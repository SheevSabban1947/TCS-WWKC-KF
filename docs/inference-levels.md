# Inference Levels

The Knowledge File uses inference levels to indicate how far a statement is from direct evidence.

Inference level does **not** measure how emotionally convincing, plausible, or narratively satisfying a claim feels. It measures the evidential distance between the claim and the source material.

A claim may feel highly plausible while still belonging to a higher inference level.

## IL-0 Raw Data / Direct Record

**Definition:**  
A source item itself, or a direct extract from a source.

This includes documents, newspaper articles, photographs, official records, maps, transcripts, direct quotations, or archived media.

**Examples:**

- A newspaper clipping mentioning Karmein Chan.
- A photograph of Karmein Chan.
- A police or coronial document.
- A direct quotation from a published interview.
- A scanned map or school document.

**Use when:**  
The record is being preserved or described as a source, not interpreted.

## IL-1 Directly Supported Fact

**Definition:**  
A factual claim directly supported by one or more reliable sources.

The source does not merely suggest the claim; it states it clearly.

**Examples:**

- Karmein Chan attended Presbyterian Ladies’ College.
- The Chan family lived at Serpells Road, Templestowe.
- Karmein Chan disappeared on 13 April 1991.
- Her remains were found in 1992.

**Use when:**  
A source explicitly states the fact.

## IL-2 Reasonable Inference

**Definition:**  
A conclusion drawn from reliable facts, context, geography, chronology, or documented patterns, but not directly stated by a source.

The inference should be explainable step by step.

**Examples:**

- Reconstructing a likely school route using known addresses, transport maps, and school location.
- Inferring that a location was significant because multiple verified events connect to it.
- Estimating a likely time window when exact timing is unavailable.

**Use when:**  
The claim is not directly documented, but the reasoning is grounded and defensible.

## IL-3 Speculative Inference

**Definition:**  
A hypothesis with some evidential grounding, but insufficient support to treat as a firm conclusion.

This level is for ideas that may help investigation or analysis but must remain clearly marked as speculative.

**Examples:**

- The offender may have had a difficult or disrupted night.
- The offender may have been confused by the Chan residence’s systems.
- The offender may have changed his mind during the attack.
- A location may have been used for observation before the crime.

**Use when:**  
The idea is plausible but cannot yet be firmly demonstrated.

## IL-4 Open Speculation / Weak Hypothesis

**Definition:**  
A weak or exploratory idea with limited evidential support.

This level may be useful for brainstorming, but it should not be presented as knowledge.

**Examples:**

- A possible suspect theory based mainly on coincidence.
- A route theory without enough geographic or documentary support.
- A psychological interpretation with minimal external evidence.

**Use when:**  
The idea is worth preserving as a question or lead, but not as a claim.

## Practical Rule

When unsure, assign the **higher** inference level.

For example:

- A direct newspaper statement is usually IL-0 or IL-1.
- A fact repeated by several reliable sources is usually IL-1.
- A reconstruction based on maps, timing, and geography is usually IL-2.
- A theory about offender intent or emotional state is usually IL-3 or IL-4.

## Recommended Data Field

Claims should include an `inference_level` field.

Example:

```json
{
  "id": "KCCLAIM0001",
  "subject_id": "KCPER0001",
  "claim": "Karmein Chan attended Presbyterian Ladies' College.",
  "inference_level": "IL-1",
  "source_refs": ["KCSRC0001"]
}
```

