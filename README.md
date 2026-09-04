# euphemism

A small, independently testable language-model judge for detecting when institutional or educational language obscures a more concrete social or economic situation.

## Task

Given a passage and source context, return:

1. literal claim;
2. concrete situation described;
3. wording that may be euphemistic;
4. plain-language rendering supported by the evidence;
5. relevant omissions;
6. plausible alternative readings;
7. evidence boundary;
8. confidence.

The judge must distinguish description from inference. It must not infer motive or bad faith unless the source supports that inference.

## Calibration

Evaluation must include positive cases, ambiguous cases, and counterexamples. The correct output may be: `no euphemistic translation justified`.

The test set should also include out-of-domain passages and cases involving people across different social positions, so success cannot come from mechanically mapping a vocabulary word to a fixed interpretation.

## Corpus records

Each item should preserve:

- exact source wording;
- source and provenance;
- surrounding context;
- proposed plain-language rendering;
- competing readings;
- evidence boundary;
- labels for training/evaluation split.

Historical and empirical claims remain tied to their underlying sources. A model score is not itself evidence for those claims.
