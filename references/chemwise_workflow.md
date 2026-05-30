# chemwise MCP Workflow (Phase 2 Regulatory Anchor)

Phase 2 establishes regulatory ground truth before any web literature search. Every claim about current EU regulatory status, EFSA conclusions, MRLs, CLP classification, or SVHC status must trace to a chemwise call cached locally.

## Call sequence

Execute in this order. Cache every response to `regulatory_anchor/chemwise/` as JSON with timestamp in filename.

### Step 1 — Identity confirmation

For each substance in scope:

1. `mcp__chemwise__search_substance` with the user-supplied name/identifier
   - Verify CAS RN, EC number, ISO common name, IUPAC match scope
   - If multiple hits, present to user via AskUserQuestion and lock the correct one
2. `mcp__chemwise__get_structure`
   - Retrieve SMILES, InChIKey
   - Record molecular formula and weight

### Step 2 — Regulatory footprint

3. `mcp__chemwise__get_registration_summary`
   - High-level registration footprint across regimes
4. `mcp__chemwise__get_regulatory_status`
   - Current status across regimes (PPP, REACH, BPR, CLP)
5. `mcp__chemwise__get_ppp_approval_status`
   - EU approval state, expiry, conditions, candidate for substitution flag
6. `mcp__chemwise__get_ppp_expiry_alerts`
   - Renewal timeline; flag if expiry within 36 months (renewal-relevant)

### Step 3 — Historical position

7. `mcp__chemwise__get_substance_review_history`
   - All prior EFSA conclusions and amendments
   - Identify supersession chain (e.g. 2017 conclusion superseded by 2023 renewal)
   - Critical for DP / reference product checks

### Step 4 — EFSA scientific record

8. `mcp__chemwise__get_efsa_conclusion_metadata`
   - Conclusion reference, publication date, RMS, version
9. `mcp__chemwise__get_efsa_conclusion_fulltext`
   - Retrieve full text for endpoint extraction
   - Mine reference list for backward citation chasing in Phase 3
10. `mcp__chemwise__search_efsa_conclusions`
    - Broader topic/endpoint discovery if scope spans multiple substances or cumulative assessment groups (CAGs)

### Step 5 — Classification and SVHC

11. `mcp__chemwise__get_cl_classification`
    - CLP Annex VI harmonised classification
    - Self-classification entries from C&L Inventory
12. `mcp__chemwise__check_svhc`
    - REACH SVHC candidate or authorisation list status
13. `mcp__chemwise__list_svhc` (only if broader SVHC sweep needed for co-formulants)

### Step 6 — Residues (if in scope)

14. `mcp__chemwise__get_mrl_status`
    - Reg 396/2005 Annex II/III/IV/V positioning
    - Article 12 review status

### Step 7 — Reference work

15. `mcp__chemwise__query_bcpc`
    - BCPC Pesticide Manual identity, mode of action, agricultural use pattern

### Step 8 — Cross-substance (optional)

- `mcp__chemwise__list_ppp_substances` with filters
   - Use when comparator search needed (e.g. all triazole fungicides, all SDHI candidates)

## Caching and provenance

Every response stored as:
```
regulatory_anchor/chemwise/<call_name>_<substance_id>_<YYYYMMDDHHMM>.json
```

Append one row to `regulatory_anchor/anchor_log.md` per call:
- Timestamp
- Tool
- Input parameters
- Output file path
- Key extracted facts (one line)

## Building anchor_summary.md

After all calls complete, synthesise into `regulatory_anchor/anchor_summary.md`:

```markdown
# Regulatory Anchor Summary - [Substance]

**Compiled:** [date]
**chemwise calls:** [n], all cached in regulatory_anchor/chemwise/

## Identity
- CAS RN:
- EC number:
- ISO common name:
- IUPAC:
- SMILES:
- InChIKey:

## Current EU PPP status
- Approval: [Y/N], approval regulation: [Reg (EU) NNNN/YYYY], expiry: [date]
- Candidate for substitution: [Y/N], date listed if Y
- Renewal status: [in progress / not started / approved / expired]

## CLP harmonised classification
[Hazard classes, categories, hazard statements, specific concentration limits]

## REACH SVHC
[Status]

## EFSA conclusions
| Conclusion | Date | RMS | Status |
|---|---|---|---|
| EFSA Journal YYYY;VV(N):NNNN | | | superseded by / current |

## MRLs (if in scope)
- Annex coverage:
- Open Article 12 review: [Y/N]
- Last MRL amendment:

## Mode of action (BCPC)
[Brief]

## Sources
- All chemwise responses cached in regulatory_anchor/chemwise/
- Timestamps as filename suffix
- Cache validity: regenerate if older than 90 days for current-status claims
```

## When chemwise output conflicts with web search

chemwise reflects the regulatory cache as maintained. If web search (EUR-Lex, EFSA Journal direct) gives a different answer:
1. Re-run the chemwise call
2. Verify against EUR-Lex / EFSA Journal via WebFetch
3. If discrepancy persists, prefer the primary source (EUR-Lex / EFSA Journal) and note the chemwise discrepancy in `LIMITATIONS.md`
4. Update memory if chemwise data quality issue is systemic

## Data protection scope add-on

If `SCOPE.md` use context = DP/reference product:
- Trigger `anthropic-skills:data-protection` skill for RR sourcing
- Use `get_substance_review_history` to build submission timeline
- Cross-reference with SharePoint DP checks index per data-protection skill workflow
- Flag any reference products where MS RR availability is unknown
