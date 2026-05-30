# Quality Appraisal Criteria

Match the tool to the study type. Record the score, the justification, and the GLP/guideline compliance flag in `EVIDENCE-TABLE.csv` for every included study.

## Klimisch reliability scoring (Klimisch et al., 1997)

Applies to in vivo and in vitro toxicology/ecotoxicology and environmental fate studies. The EU baseline for regulatory reliability.

| Score | Label | Criteria |
|---|---|---|
| 1 | Reliable without restriction | GLP, OECD or equivalent guideline, full reporting, QA statement, no significant deviations |
| 2 | Reliable with restrictions | Guideline-aligned but minor deviations; or non-GLP but well-documented and scientifically sound; or pre-guideline study with adequate detail |
| 3 | Not reliable | Significant deficiencies in design or reporting; conflicting results; insufficient documentation |
| 4 | Not assignable | Abstract only; secondary citation; insufficient information to evaluate |

**Justification text** is mandatory. Record specifically what the study did or did not do that drives the score.

## ToxRTool (Schneider et al., 2009)

Structured Klimisch supplement for in vivo and in vitro tox. 18-21 criteria (in vivo) covering test substance ID, test system, study design, results, conclusions. Use for borderline Klimisch 1/2 calls.

## CRED (Criteria for Reporting and Evaluating ecotoxicity Data; Moermond et al., 2016)

Ecotoxicology equivalent of ToxRTool. Separate reliability and relevance scoring. Required by ECHA REACH guidance and EFSA PPR ecotox guidance for non-standard studies.

## OHAT Risk of Bias (NTP/OHAT, 2019)

For human and animal observational and experimental studies in environmental health epidemiology. Eleven RoB domains rated definitely low / probably low / probably high / definitely high.

Use when including epidemiology in mammalian tox or ED assessment.

## Navigation Guide

Alternative for systematic reviews of environmental health epidemiology. Compatible with OHAT.

## AMSTAR-2 (Shea et al., 2017)

For appraising included systematic reviews. 16 items; overall confidence rated high / moderate / low / critically low based on weaknesses in critical domains (study selection, RoB assessment of primary studies, statistical methods, publication bias, conflicts of interest).

## ROBIS

Alternative SR appraisal tool. Three phases (relevance, concerns, overall RoB). Use when AMSTAR-2 ambiguous.

## OECD QSAR validation principles (OECD, 2007)

For QSAR / in silico predictions:
1. Defined endpoint
2. Unambiguous algorithm
3. Defined domain of applicability
4. Appropriate measures of goodness-of-fit, robustness, predictivity
5. Mechanistic interpretation if possible

Document via QMRF (QSAR Model Reporting Format) and QPRF (QSAR Prediction Reporting Format).

## ECHA RAAF (Read-Across Assessment Framework)

For read-across justifications. Six scenarios (analogue or category, with/without trend). Required for REACH and increasingly for PPP co-formulant assessments.

## OECD GD 286 / GIVIMP

Good In Vitro Method Practices. Use for evaluating NAMs (new approach methodologies) including ED screening assays (OECD CF on ED).

## EURL ECVAM validation status

Cross-reference NAMs against the EURL ECVAM Tracking System for Alternative methods towards Regulatory acceptance (TSAR). Methods at EURL ECVAM validated status carry the highest regulatory weight among NAMs.

## FOCUS scenario compliance

Environmental fate modelling outputs (PEC soil, PECsw, PECgw) must use FOCUS scenarios (FOCUSsw Step 1-4, FOCUSgw PEARL/PELMO) and approved input parameters. Non-FOCUS modelling carries lower weight.

## OECD 307/308 conformity

For soil and water-sediment metabolism studies. Report DT50, DT90, kinetic fit (SFO, FOMC, DFOP, HS, IORE) and goodness-of-fit metrics (chi-square error <15% per FOCUS Kinetics).

## OECD 509 / GAP alignment

For supervised residue field trials. Confirm GAP (rate, timing, PHI, number of applications) matches the GAP being supported. Off-GAP trials require justification.

## Reporting standards for primary literature

| Study type | Reporting standard |
|---|---|
| Animal in vivo (preclinical) | ARRIVE 2.0 |
| RCT human | CONSORT |
| Observational human | STROBE |
| Systematic review | PRISMA 2020 |
| Diagnostic accuracy | STARD |

Studies failing the reporting standard for their type are downgraded Klimisch by one step.

## Overall reliability decision rules

A study is suitable as a key study (drives the regulatory endpoint) only if:
- Klimisch 1 or 2 with documented justification
- Guideline-compliant or scientifically justified deviation
- GLP, or non-GLP with explicit QA equivalence statement
- COI declared
- Reporting standard met

Studies failing these are supporting evidence at best, or excluded.
