# SEARCH LOG — [Substance / Topic]

One entry per database query. Append-only; do not edit historical entries.

## Entry template

```
### [Database name] - [endpoint block] - [YYYY-MM-DD HH:MM]

- URL / interface:
- Query string (verbatim):
- Field tags / controlled vocabulary used:
- Filters: [date range, language, study type, document type]
- Hit count returned:
- Records exported: n =
- Export format: [RIS / BibTeX / CSV / JSON]
- Exported to file:
- Action: [screen / cite-chase / superseded by query Y]
- Notes:
```

## Worked example

### chemwise.search_efsa_conclusions - mammalian tox endpoint discovery - 2026-05-29 10:14

- URL: MCP tool (mcp__chemwise__search_efsa_conclusions)
- Query: substance = "glyphosate"; endpoint_keywords = ["NOAEL", "developmental"]
- Filters: none
- Hit count: 12
- Records exported: 12
- Export format: JSON
- File: regulatory_anchor/chemwise/efsa_conclusions_glyphosate.json
- Action: full-text retrieval via get_efsa_conclusion_fulltext for top 3 by relevance
- Notes: 2023 conclusion supersedes 2017 for renewal endpoints; flag both for version comparison.

### PubMed - aquatic toxicity - 2026-05-29 11:02

- URL: https://pubmed.ncbi.nlm.nih.gov/
- Query: `("glyphosate"[Title/Abstract] OR "N-(phosphonomethyl)glycine"[Title/Abstract] OR "1071-83-6"[All Fields]) AND ("fish"[MeSH] OR "Daphnia"[MeSH] OR "aquatic toxicity"[Title/Abstract]) AND 2015:2026[PDAT]`
- Field tags: [Title/Abstract], [MeSH], [PDAT]
- Filters: English; humans/animals filter off (need non-mammalian)
- Hit count: 342
- Records exported: 342 (RIS)
- File: searches/pubmed_glyphosate_aquatic_20260529.ris
- Action: deduplicate against WoS + Scopus exports; title screen
- Notes: includes formulation studies; tag formulation vs technical at full-text stage.
