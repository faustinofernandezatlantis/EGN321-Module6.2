# AI_LOG.md

Tool: Ollama
Model: qwen2.5:0.5b

## Purpose
Use a local small language model to review deterministic comparison evidence,
challenge conclusions, propose testable hypotheses, and help draft the report.

## Deterministic evidence
Comparable points: 1747
Mean signed difference: 1.735 degrees C
Mean absolute difference: 1.735 degrees C
Maximum absolute difference: 2.603 degrees C

Status counts:
{'OK': 1747, 'MISSING': 33, 'REJECTED': 14, 'SUSPICIOUS': 6}

## AI tasks performed
1. Proposed hypotheses from supplied evidence.
2. Red-teamed a provisional conclusion.
3. Drafted a report using the supplied evidence and review notes.

## Verification rule
AI output is not treated as evidence.
Claims must be verified against Python results, plots, source data, or a new deterministic test.

## Instructor/student review

- **Which AI suggestions were accepted?**
  - The AI's identification of a persistent positive offset across samples as evidence for sensor calibration error / thermal self-heating.
  - The suggested structure for comparing evidence, missing evidence, and proposed verification tests.

- **Which were rejected?**
  - The AI's drafted conclusion claiming that the +1.735 °C mean signed difference was "not statistically significant" or "within margin of error". Across 1,747 valid points, a persistent positive residual is a clear systematic bias, not random noise.

- **What deterministic test was added?**
  - A 2-point reference calibration test (ice water bath at 0 °C and boiling water at 100 °C) against a calibrated reference instrument to confirm or reject the offset hypothesis.

- **What changed in the final report?**
  - Corrected all incorrect statistical claims made in the Ollama draft.
  - Replaced the hallucinated AI conclusions with accurate observations directly backed by Python residual calculations and generated plots.