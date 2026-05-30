---
name: ppp-literature-review
description: Rigorous, defensible literature reviews for EU plant protection product (PPP) regulatory work on active substances, metabolites, co-formulants, formulations. Use for literature reviews, evidence synthesis, hazard ID, risk analysis, data gap analysis vs Reg 283/284/2013, MRL review, Article 12 review, dossier/RAR support, renewal preparation, endocrine disruptor (ED) assessment, substitution assessment, data protection / reference product checks, weight-of-evidence (WoE), mode-of-action review. Sources tiered by regulatory defensibility (EFSA/ECHA/RMS first, peer-reviewed second, grey literature last); citations verified pre-delivery; EFSA-style writing. Triggers: "lit review", "PPP review", "evidence synthesis", "what does EFSA say about", "data gap analysis", "WoE for", "ED assessment", "DP check", "RAR literature", "MRL review", "Article 12 review", "/lit-review", "/ppp-review", "/evidence-synthesis".
allowed-tools: Read, Write, Edit, Grep, Glob, Bash, WebSearch, WebFetch, AskUserQuestion, mcp__chemwise__search_substance, mcp__chemwise__get_registration_summary, mcp__chemwise__get_regulatory_status, mcp__chemwise__get_ppp_approval_status, mcp__chemwise__get_ppp_expiry_alerts, mcp__chemwise__get_mrl_status, mcp__chemwise__get_efsa_conclusion_metadata, mcp__chemwise__get_efsa_conclusion_fulltext, mcp__chemwise__search_efsa_conclusions, mcp__chemwise__get_cl_classification, mcp__chemwise__check_svhc, mcp__chemwise__list_svhc, mcp__chemwise__get_substance_review_history, mcp__chemwise__query_bcpc, mcp__chemwise__get_structure, mcp__chemwise__list_ppp_substances
metadata:
    skill-author: Dylan Grimes Larkin (Regulatory Scientist @ Life Scientific)
    domain: EU PPP Regulatory affairs/science
    version: 1.0
---

# PPP Literature Review

## Purpose

Produce literature reviews suitable for EU regulatory submissions, internal scientific decisions, and legal defensibility. Diligence, accuracy, completeness, and traceable citation are non-negotiable. Output must withstand scrutiny from EFSA peer review, RMS evaluators, and competent authority audits.

## When to Use

Trigger when the user requests any of:
- Literature review, evidence synthesis, state-of-the-art summary
- Hazard identification, hazard characterisation
- Risk analysis, risk characterisation, weight-of-evidence (WoE)
- Endpoint review (tox, ecotox, fate, residue, efficacy)
- Data gap analysis vs Reg 283/2013 or 284/2013
- MRL review or setting support
- Article 12 MRL review, Article 43 product re-authorisation
- Renewal dossier (RAR/DAR) literature support
- Endocrine disruptor (ED) assessment under Reg 2018/605
- Substitution candidate evaluation under Reg 2015/408
- Data protection / data exclusivity / reference product check
- Comparative assessment, mode-of-action review
- Co-formulant review under REACH
- Regulatory position defence, dispute, or precedent search

Do NOT use for: quick factual lookups (use chemwise directly), single-document summary, drafting non-literature regulatory text.

## Operating Principles

1. **Regulatory truth precedes peer-reviewed truth.** EFSA conclusion or RMS RAR overrides journal paper on contested endpoints.
2. **Cite or omit.** Every quantitative claim, regulatory statement, and study reference carries an inline citation resolving to a verifiable source. No orphan claims.
3. **Tier every source.** Source tier governs weight. Tier and Klimisch (or equivalent) recorded per included item.
4. **Document the negative space.** Excluded studies, failed queries, and data gaps are logged as carefully as included findings.
5. **Calibrated language.** Hedging matches evidence weight. Absolutes only where legislation defines them.
6. **Reproducibility.** Search strings, dates, databases, hit counts captured verbatim in `SEARCH-LOG.md`.

## Writing Conventions (enforced)

- Third person. Past tense for findings, present tense for established knowledge and current regulatory status.
- No em-dashes or en-dashes. Use single hyphens, parentheses, commas, periods.
- No subjective, informal, ambiguous, vague, or passive-leaning language where active is clearer.
- No exaggeration. Match language to evidence weight: "demonstrated" (multi-study, Klimisch 1, replicated) vs "indicated" (single study) vs "reported but not independently confirmed".
- Quantitative anchors required: NOAEL/LOAEL/NOEC/LD50 with units, n, route, species, study duration, CI where reported.
- Acronyms expanded on first use; glossary appended.
- Distinguish source voice explicitly: "EFSA concluded …" vs "the applicant reported …" vs "one peer-reviewed study found …" vs "industry task force documents suggest …".

## Workflow

Execute phases sequentially. Do not skip Phase 1 or Phase 6.

### Phase 1: Scope Lock (mandatory gate)

Use `AskUserQuestion` to lock scope before any searching. Capture:

1. **Question type**: hazard ID | hazard characterisation | exposure | risk analysis | risk characterisation | data gap | MRL review | DP/reference product | ED assessment | substitution | renewal | efficacy/resistance | mode of action | regulatory precedent
2. **PECO-R framework** (adapted PICO):
   - **P**opulation: target organism / human subpopulation / environmental compartment / matrix
   - **E**xposure: substance + route + duration + concentration range
   - **C**omparator: control, reference substance, baseline GAP, regulatory threshold
   - **O**utcome: endpoint(s), measured parameters
   - **R**egulatory context: which instrument(s), which Annex point(s), which jurisdiction
3. **Substance scope**: active substance(s), metabolites of interest, co-formulants, formulation type, CAS RN, EC number, ISO common name, IUPAC, SMILES/InChIKey
4. **Endpoint scope**: specific Annex II/III data points; or open if exploratory
5. **Geography/jurisdiction**: EU-wide | zonal (N/C/S) | specific MS | global comparator
6. **Time window**: default last 10 years; full historical for renewal/ED/substitution
7. **Use context**: dossier (new/renewal/Art.43) | MRL | Art.12 review | DP check | internal R&D | litigation defence | scientific opinion drafting
8. **Depth tier**:
   - **Rapid scoping** (~1 day equivalent): chemwise + EFSA + 1 academic database, top-20 papers per endpoint, no dual screening
   - **Structured** (default, ~1 week): chemwise + EFSA + ECHA + 3 academic databases + grey lit, full PRISMA flow, single reviewer with documented exclusions
   - **Systematic (PRISMA-grade)**: all of above + dual-screening simulation (two independent passes with different lens), formal RoB, AMSTAR-2 for included SRs
9. **Output format**: Markdown only | Markdown + Word (.docx via `anthropic-skills:docx`) | Both
10. **Citation style**: EFSA (default) | Vancouver | APA

Write captured scope to `SCOPE.md` at top of working directory. Block downstream phases until user confirms.

### Phase 2: Regulatory Anchor (chemwise-first)

Before any web search, establish regulatory ground truth via chemwise MCP. Cache results to `regulatory_anchor/`:

For each substance in scope, execute (in parallel where independent):

1. `mcp__chemwise__search_substance` → confirm identity, retrieve synonyms, CAS/EC/ISO mapping
2. `mcp__chemwise__get_structure` → InChIKey, SMILES, structural validation
3. `mcp__chemwise__get_registration_summary` → registration footprint
4. `mcp__chemwise__get_regulatory_status` + `mcp__chemwise__get_ppp_approval_status` → current EU approval state, expiry, conditions
5. `mcp__chemwise__get_ppp_expiry_alerts` → renewal timeline context
6. `mcp__chemwise__get_substance_review_history` → version control of regulatory position
7. `mcp__chemwise__get_efsa_conclusion_metadata` → EFSA peer review record
8. `mcp__chemwise__get_efsa_conclusion_fulltext` → conclusion text for endpoint extraction
9. `mcp__chemwise__get_mrl_status` → if residue/MRL in scope
10. `mcp__chemwise__get_cl_classification` → CLP harmonised classification
11. `mcp__chemwise__check_svhc` → REACH SVHC cross-check
12. `mcp__chemwise__query_bcpc` → BCPC Pesticide Manual entry

If scope = DP/reference product, additionally trigger `anthropic-skills:data-protection` for RR sourcing and cross-reference with substance review history for submission timeline.

Cross-jurisdictional endpoint discovery (broader than single substance):
- `mcp__chemwise__search_efsa_conclusions` with endpoint/topic keywords
- `mcp__chemwise__list_ppp_substances` with filter criteria if comparator search

For legislative anchoring, resolve via `assets/eu_ppp_regulations.json` (lookup by CELEX; fields: `celex`, `type`, `number`, `short_title`, `category`, `status`, `subject`, `local_md`, `eurlex_page`, `eurlex_html`, `eurlex_pdf`). Read the `local_md` file directly. Do not WebFetch EUR-Lex when local copy exists. Cite as CELEX (e.g. `Reg (EC) 1107/2009, Art. 4(1) [CELEX:32009R1107]`).

For guidance citation, consult `references/PPP_Guidance_Documents_Reference.md`, `references/PPP_National_Guidance_Documents_Reference.md`, and `references/OECD_Test_Guidelines_Reference.md` for canonical document IDs. OECD Test Guideline PDF URLs are resolved via `assets/oecd_test_guidelines.json` (lookup by `section` + `tg_num`; fields: `title`, `page_url`, `pdf_url`, `pubid`). Fetch on demand with WebFetch using the `pdf_url` field; do not bundle PDFs.

Output of Phase 2: `regulatory_anchor/anchor_summary.md` containing identity, current status, key EFSA conclusion endpoints, classification, and dated source list. This is the spine the rest of the review hangs on.

### Phase 3: Tiered Literature Search

Build search blocks from PECO-R. Run searches in tier order so higher-tier sources establish the canonical claims first.

**Tier 1 — Regulatory primary** (already partially complete via Phase 2)
- EFSA Journal full-text (via chemwise + WebFetch for non-cached opinions)
- EFSA OpenFoodTox endpoints
- ECHA: RAC/SEAC opinions, CLH dossiers, REACH registration dossiers
- EU Pesticides Database
- RMS DAR/RAR (cite RMS, year, version)
- MS competent authority registers (BVL, ANSES, CTGB, HSE, etc.)
- JMPR/JECFA monographs, Codex MRLs
- OECD Test Guidelines and monographs (index: `references/OECD_Test_Guidelines_Reference.md`; URL resolver: `assets/oecd_test_guidelines.json`; fetch PDFs on demand via WebFetch)

**Tier 2 — Authoritative secondary**
- US EPA (regulations.gov dockets, OPP risk assessments)
- PMRA (Canada), APVMA (Australia), FAO
- IARC monographs, NTP, WHO/IPCS EHC
- IUCLID extracts, eChemPortal
- BCPC Pesticide Manual, PPDB (Hertfordshire), BPDB

**Tier 3 — Peer-reviewed primary literature**
Search via `WebSearch` and `WebFetch`. Priority journals:
- J. Agric. Food Chem.
- Pest Manag. Sci.
- Environ. Toxicol. Chem.
- Chemosphere
- Sci. Total Environ.
- Regul. Toxicol. Pharmacol.
- Crit. Rev. Toxicol.
- Food Chem. Toxicol.
- Arch. Toxicol.
- EFSA Journal
- Environ. Sci. Technol.
- Ecotoxicol. Environ. Saf.

Search identifier-first: CAS RN, EC number, ISO common name. Avoid trade-name-only queries.

Use Boolean blocks: `(substance OR synonyms) AND (endpoint OR endpoint_synonym) AND (population OR matrix) AND (year_filter)`.

Backward and forward citation chasing from EFSA conclusion bibliography is highest yield. Mine EFSA conclusion reference lists first.

**Tier 4 — Grey literature** (cite with tier flag)
- Industry task force reports (ECPA/CropLife)
- Conference proceedings (SETAC, BCPC Congress, IUPAC)
- Theses (only if cited by Tier 1-3 sources)
- Preprints (label clearly as non-peer-reviewed; verify final publication status)

**Default rejection** (do not cite):
- Predatory journals (Beall/Cabells check)
- Non-English without verified translation
- Blog posts, advocacy NGO claims unless triangulated against Tier 1-2
- Trade press except for factual market context

Document every search in `SEARCH-LOG.md` using `assets/search_log_template.md`:
- Database, date, exact query string, filters, hit count, action taken (export N, screen N)

### Phase 4: Screening and Selection

1. **Deduplicate** by DOI primary, then fuzzy title match across all collected hits.
2. **Title screening** against PECO-R inclusion/exclusion criteria from `SCOPE.md`. Log every exclusion with reason code (lang | scope | endpoint | quality | duplicate | predatory).
3. **Abstract screening** with same criteria.
4. **Full-text screening** with detailed criteria including study-design quality flags.
5. For **systematic tier**: simulate dual screening by running two independent passes with different framing (hazard-first vs exposure-first). Note disagreement rate as limitation.
6. Build PRISMA 2020 flow diagram from `assets/prisma_template.md`. Write to `PRISMA-FLOW.md`.

### Phase 5: Quality Appraisal

Apply study-type-matched tools to each included study. Record in `EVIDENCE-TABLE.csv` (template at `assets/evidence_table_template.csv`):

| Study type | Primary tool | Secondary | Compliance flag |
|---|---|---|---|
| In vivo mammalian tox | Klimisch (1-4) | ToxRTool | OECD TG + GLP |
| Ecotoxicology | Klimisch | CRED (Moermond) | OECD TG + GLP |
| Epidemiology | OHAT RoB | Navigation Guide | STROBE/CONSORT |
| In vitro / NAMs | OECD GD 286 | EURL ECVAM validation | GIVIMP |
| Environmental fate | FOCUS scenario alignment | OECD 307/308 conformity | OECD TG + GLP |
| Residue field trials | OECD 509 | GAP alignment | OECD TG + GLP |
| Systematic reviews | AMSTAR-2 | ROBIS | PRISMA compliance |
| QSAR / in silico | OECD QSAR validation principles (5 OECD principles) | REACH Annex XI 1.3 | OECD QMRF |
| Read-across | ECHA RAAF | - | OECD Adverse Outcome Pathway |

For each included study record: source tier, Klimisch (or equivalent), GLP Y/N, guideline-compliant Y/N, deviations, conflict-of-interest flag (industry-funded | regulator | independent academic | undisclosed).

Detailed criteria in `references/quality_appraisal.md`.

### Phase 6: Thematic Synthesis

Synthesise across studies, never study-by-study. Required structure for the main `REVIEW.md`:

1. **Executive summary** (max 1 page)
2. **Regulatory context** — cite from `assets/eu_ppp_regulations/` and Phase 2 anchor
3. **Substance identity and physicochemical properties**
4. **Mode of action / mechanism** (if relevant)
5. **Hazard profile**
   - 5.1 Mammalian toxicology by endpoint (ADME, acute, repeat-dose, repro/dev, genotox, carcinogenicity, neurotox, ED)
6. **Ecotoxicology** by taxonomic group (aquatic vertebrates, invertebrates, algae, bees, non-target arthropods, earthworms, soil microorganisms, birds, mammals, non-target plants)
7. **Environmental fate and behaviour** (soil, water, air, photolysis, hydrolysis, metabolism, leaching, PEC modelling)
8. **Residues and dietary exposure** (plant metabolism, livestock metabolism, processing, MRL coverage, dietary risk)
9. **Efficacy and resistance** (if in scope)
10. **Cross-jurisdictional risk assessment outcomes** (EU vs US vs other)
11. **Weight-of-evidence integration** — explicit WoE per endpoint per EFSA WoE guidance
12. **Data gaps and uncertainties** mapped to Reg 283/2013 and 284/2013 data point IDs
13. **Regulatory implications**
14. **Limitations of this review**

Each section requires cross-study tables (endpoint × species × value × source × tier × Klimisch × GLP).

Hedging calibration:
- "Demonstrated" / "established": ≥2 Klimisch 1 GLP studies, consistent direction, replicated independently
- "Indicated" / "supported by": single Klimisch 1 or multiple Klimisch 2
- "Reported": single Klimisch 2-3, or grey literature triangulated
- "Suggested but not confirmed": Klimisch 3-4 only, or unreplicated peer-reviewed claim
- Never use "proven", "definitive", "conclusive" unless EFSA conclusion or harmonised classification supports

Template at `assets/review_template.md`.

### Phase 7: Citation Verification

Mandatory before delivery. For each citation:
1. Resolve DOI or URL (WebFetch each, log status)
2. Verify author list, title, year, journal, volume, pages match
3. Confirm cited claim actually appears at the cited location
4. For EFSA conclusions: verify document version and publication date
5. For legislation: verify CELEX number and current consolidated status (note: amended texts may differ from original)

Failed citations: fix or remove. Re-verify until pass rate = 100%.

Output: `CITATION-LEDGER.md` with one row per cited source: claim summary | source | location (page/section/DOI fragment) | verified date | tier | COI flag.

### Phase 8: Output Delivery

Generate artefact set in working directory:
- `REVIEW.md` — main narrative
- `SCOPE.md` — locked scope (Phase 1)
- `SEARCH-LOG.md` — queries and database hits
- `PRISMA-FLOW.md` — screening counts
- `EVIDENCE-TABLE.csv` — per-study structured data
- `CITATION-LEDGER.md` — verified citation registry
- `BIBLIOGRAPHY.bib` — BibTeX with `tier`, `klimisch`, `glp`, `guideline` custom fields
- `GAPS.md` — data gaps mapped to Reg 283/284 data points
- `LIMITATIONS.md` — methodological caveats
- `regulatory_anchor/` — Phase 2 cached outputs

If user selected Word output, invoke `anthropic-skills:docx` skill on `REVIEW.md` to produce `.docx` deliverable with EFSA-style formatting (Times New Roman 11pt or Arial 11pt, justified body, numbered headings, footnote citations).

## Source Hierarchy Quick Reference

See `references/source_hierarchy.md` for full criteria. Summary order of weight for contested claims:

1. EFSA Conclusion (peer-reviewed by MS)
2. ECHA RAC opinion (for CLH)
3. RMS RAR/DAR
4. EFSA Scientific Opinion
5. OECD monograph / JMPR evaluation
6. EU MS competent authority assessment
7. EPA / PMRA / APVMA risk assessment
8. Peer-reviewed primary literature in Tier-1 specialist journal, Klimisch 1, GLP
9. Peer-reviewed primary literature, Klimisch 2
10. Industry task force grey literature (with COI flag)
11. Preprint (with non-peer-review flag)
12. Other grey

When sources conflict, higher tier wins unless the lower-tier source post-dates the higher-tier one and presents new data. Document conflict resolution explicitly.

## Common Pitfalls

1. **Skipping Phase 2 regulatory anchor.** Leads to peer-reviewed claims contradicting current EFSA position without acknowledgement.
2. **Trade-name searches.** Miss the substance under CAS/ISO. Always identifier-first.
3. **Single-database peer-reviewed search.** Misses substance literature in agronomy vs toxicology databases.
4. **Treating preprints as peer-reviewed.** Always flag and verify final publication.
5. **Ignoring metabolite literature.** Most fate/residue claims hinge on metabolites; search them separately.
6. **Citing repealed legislation.** Always confirm in-force status (e.g. Reg 1185/2009 repealed by Reg 2022/2379 from 2025).
7. **Confusing approval status with authorisation status.** Active substance approval (EU level) ≠ product authorisation (MS level).
8. **Failing to distinguish original vs amended text** when citing data requirements regulations.
9. **Quantitative claim without units, species, route, duration.**
10. **Synthesising study-by-study instead of thematically.**

## Bundled Resources

**Templates** (`assets/`):
- `review_template.md` — full review structure
- `prisma_template.md` — PRISMA 2020 flow
- `search_log_template.md` — reproducible search documentation
- `evidence_table_template.csv` — per-study data extraction
- `scope_template.md` — Phase 1 capture

**References** (`references/`):
- `source_hierarchy.md` — tiering rationale and authoritative source list
- `quality_appraisal.md` — Klimisch, OHAT, AMSTAR-2, OECD criteria
- `eu_regulatory_framework.md` — instrument summary, when to cite which
- `chemwise_workflow.md` — Phase 2 MCP call sequence and caching
- `citation_styles_ppp.md` — EFSA, Vancouver, APA examples for regulatory and journal sources

**Regulatory corpus** (`assets/`):
- `assets/eu_ppp_regulations.json` — EU legislation resolver (CELEX → local markdown + EUR-Lex URLs). Lookup keys: `celex`. Use `local_md` for offline read; `eurlex_html` / `eurlex_pdf` for live fetch if local missing or for adjacent legislation landing-page entries.
- `assets/eu_ppp_regulations/` — markdown copies of all instruments listed in the scope table (converted from EUR-Lex HTML); cite locally before fetching EUR-Lex.
- `assets/oecd_test_guidelines.json` — OECD TG URL resolver (section, tg_num, title, page_url, pdf_url, pubid). Use for `WebFetch` of the canonical PDF when guideline-compliance verification or direct quoting needed.

**Reference indexes** (`references/`):
- `references/PPP_Guidance_Documents_Reference.md` — SANCO/SANTE, FOCUS, EFSA, EPPO guidance index
- `references/PPP_National_Guidance_Documents_Reference.md` — MS competent authority guidance index
- `references/OECD_Test_Guidelines_Reference.md` — OECD TG index mapped to the `assets/oecd-test-guidelines/` PDF corpus

## Integration

- **chemwise MCP** — primary regulatory data source (Phase 2 spine)
- **anthropic-skills:data-protection** — RR sourcing for DP scope
- **anthropic-skills:docx** — Word deliverable
- **anthropic-skills:m365-email-search** — retrieve prior internal correspondence on substance if relevant
- **WebSearch / WebFetch** — Tier 2-4 sources

## Quality Checklist (pre-delivery)

- [ ] Scope locked in `SCOPE.md` and confirmed by user
- [ ] chemwise anchor complete for every in-scope substance
- [ ] Every endpoint claim tier-tagged
- [ ] PRISMA flow diagram complete
- [ ] All citations verified (100% pass)
- [ ] Evidence table complete with Klimisch/equivalent per study
- [ ] Data gaps mapped to Reg 283/284 data point IDs
- [ ] No em-dashes / en-dashes
- [ ] No absolute language unmatched to evidence weight
- [ ] Source voice attributed explicitly (EFSA vs applicant vs author)
- [ ] Repealed/amended legislation flagged correctly
- [ ] Conflict-of-interest flags on industry-funded sources
- [ ] Limitations section drafted

Review fails if any box unchecked. Do not deliver.
