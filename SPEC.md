# Judge contract

## Input

```text
passage: exact words under review
context: enough surrounding text to interpret the passage
source: citation or provenance record
question: optional specific interpretive question
```

## Output

The judge returns one record with these fields:

```yaml
literal_claim: ""
concrete_situation:
  people: []
  resources: []
  obligations: []
  dependencies: []
  institutions: []
possible_euphemisms:
  - wording: ""
    obscures: ""
    support: ""
plain_language_rendering: ""
omissions: []
alternative_readings: []
evidence_boundary: []
confidence:
  situation: 0.0
  euphemism: 0.0
```

## Interpretation rules

### 1. Reconstruct before translating

First describe the concrete situation without assigning intent. For education-related passages this may include whether a family owns enough property or wealth to support a child without wages, whether the child is expected to earn a living, who controls access to schooling or employment, and what economic choices are realistically available.

### 2. Euphemism is a relation, not a word list

Words such as `opportunity`, `uplift`, `unfortunate`, `poor`, `underserved`, `mobility`, or `human capital` are not euphemisms by definition. They become candidates only when the context shows that the wording abstracts, softens, moralizes, or hides a more concrete relation or condition.

### 3. Do not infer motive from effect

A phrase may obscure a material condition without the speaker deliberately intending to obscure it. The output must keep these claims separate:

- the wording has an obscuring effect;
- the speaker intended that effect;
- the speaker was dishonest.

Only the first can normally be inferred from wording alone.

### 4. Preserve material asymmetries

When supported by the source, the reconstruction should name asymmetries that abstract language can erase: ownership, wealth, dependence on wages, bargaining power, access to credentials, institutional authority, ability to refuse an offer, and exposure to risk.

### 5. Do not make education causal by default

A statement that one educational category earns more than another is not, by itself, proof that schooling caused the difference. The judge should distinguish an observed category difference from causal claims and note plausible selection, prior wealth, status, geography, occupation, family resources, and other confounding factors when relevant.

### 6. Refusal is a valid result

If the stronger rendering is not supported, return:

```text
plain_language_rendering: no euphemistic translation justified
```

and explain why.

## Evaluation

A useful test suite should score at least four independent behaviors:

1. **literal fidelity** — does the judge preserve what was actually said?
2. **material reconstruction** — does it identify concrete conditions supported by context?
3. **overreach control** — does it refuse motive, conspiracy, or causal claims not in evidence?
4. **counterexample behavior** — can it leave superficially similar wording untranslated when context does not support the euphemistic reading?

Report these separately rather than collapsing them into one accuracy number.

## Out-of-distribution tests

Feed the judge passages containing familiar trigger words in unrelated contexts, passages describing wealthy or high-status people in distress, neutral statistical prose, satire, quoted historical language, and passages where the speaker explicitly states the supposedly hidden material relation. Record whether the model bends them toward its training theme.

The target is not ideological neutrality in the abstract. The target is a falsifiable interpretive instrument whose characteristic errors can be measured.