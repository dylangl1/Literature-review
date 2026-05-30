# Citation Styles for PPP Literature Reviews

EFSA style is default. Vancouver and APA available on request. Every citation must include a resolver (DOI, CELEX, URL) plus accessed date for online sources.

## EFSA style (default)

### In-text
- Single author: (Smith, 2019)
- Two authors: (Smith and Jones, 2019)
- Three or more: (Smith et al., 2019)
- EFSA opinion: (EFSA, 2023)
- Legislation: (Reg (EC) 1107/2009)

### Reference list

**Journal article:**
> Smith, J., Jones, M., Williams, K., 2019. Aquatic toxicity of substance X to Daphnia magna under semi-static conditions. Environmental Toxicology and Chemistry, 38(4), 712-721. https://doi.org/10.1002/etc.4357

**EFSA conclusion:**
> EFSA (European Food Safety Authority), 2023. Conclusion on the peer review of the pesticide risk assessment of the active substance glyphosate. EFSA Journal 2023;21(7):8164, 245 pp. https://doi.org/10.2903/j.efsa.2023.8164

**EFSA scientific opinion:**
> EFSA PPR Panel (EFSA Panel on Plant Protection Products and their Residues), 2013. Scientific Opinion on the developmental neurotoxicity potential of acetamiprid and imidacloprid. EFSA Journal 2013;11(12):3471, 47 pp. https://doi.org/10.2903/j.efsa.2013.3471

**EFSA reasoned opinion (MRL):**
> EFSA, 2022. Reasoned Opinion on the modification of the existing maximum residue levels for substance Y in various crops. EFSA Journal 2022;20(N):NNNN.

**RAR / DAR:**
> RMS (Member State Rapporteur), 2021. Renewal Assessment Report on substance X, Volume 3 B.6 Toxicology, Rev. 2, June 2021. Submitted to EFSA under Regulation (EU) 2020/1740.

**ECHA RAC opinion:**
> ECHA RAC (Risk Assessment Committee), 2020. Opinion proposing harmonised classification and labelling at EU level of substance X. ECHA/RAC/CLH-O-0000006995-78-01/F, adopted 4 June 2020.

**EU legislation:**
> European Commission, 2009. Regulation (EC) No 1107/2009 of the European Parliament and of the Council of 21 October 2009 concerning the placing of plant protection products on the market. OJ L 309, 24.11.2009, p. 1-50. CELEX:32009R1107.

**OECD Test Guideline:**
> OECD, 2018. Test No. 211: Daphnia magna Reproduction Test. OECD Guidelines for the Testing of Chemicals, Section 2, OECD Publishing, Paris. https://doi.org/10.1787/9789264070127-en

**OECD monograph:**
> OECD, 2014. Guidance Document on the validation of (Quantitative) Structure-Activity Relationship [(Q)SAR] models. OECD Series on Testing and Assessment, No. 69, ENV/JM/MONO(2007)2.

**JMPR monograph:**
> JMPR (Joint FAO/WHO Meeting on Pesticide Residues), 2016. Pesticide residues in food 2016: Toxicological evaluations. FAO Plant Production and Protection Paper 229.

**Book / technical manual:**
> MacBean, C. (Ed.), 2012. The Pesticide Manual, 16th ed. BCPC, Alton, UK.

**Database entry (BCPC, PPDB):**
> University of Hertfordshire, 2024. Pesticide Properties DataBase (PPDB): substance X. https://sitem.herts.ac.uk/aeru/ppdb/, accessed 2026-05-29.

**Preprint:**
> Smith, J., 2024. Title of preprint [preprint, not peer-reviewed]. bioRxiv 2024.01.15.123456. https://doi.org/10.1101/2024.01.15.123456

**Industry task force report (grey, COI flagged):**
> Crop Protection Industry Task Force, 2018. Cumulative assessment group dossier for triazoles [industry-sponsored grey literature]. Report TF-2018-014, ECPA.

## Vancouver

### In-text
Superscript numbers in citation order: text¹²,³.

### Reference list
> 1. Smith J, Jones M, Williams K. Aquatic toxicity of substance X to Daphnia magna. Environ Toxicol Chem. 2019;38(4):712-21. doi:10.1002/etc.4357

## APA 7th

### In-text
- (Smith et al., 2019)
- (EFSA, 2023)

### Reference list
> Smith, J., Jones, M., & Williams, K. (2019). Aquatic toxicity of substance X to Daphnia magna under semi-static conditions. *Environmental Toxicology and Chemistry*, *38*(4), 712-721. https://doi.org/10.1002/etc.4357

## BibTeX custom fields

For `BIBLIOGRAPHY.bib`, extend standard BibTeX with PPP-relevant fields:

```bibtex
@article{smith2019,
  author = {Smith, J. and Jones, M. and Williams, K.},
  title = {Aquatic toxicity of substance X to Daphnia magna under semi-static conditions},
  journal = {Environmental Toxicology and Chemistry},
  year = {2019},
  volume = {38},
  number = {4},
  pages = {712-721},
  doi = {10.1002/etc.4357},
  tier = {3},
  klimisch = {1},
  glp = {Y},
  guideline = {OECD TG 211},
  coi = {IND-NOTIFIED},
  accessed = {2026-05-29}
}

@misc{efsa2023glyphosate,
  author = {{EFSA}},
  title = {Conclusion on the peer review of the pesticide risk assessment of the active substance glyphosate},
  year = {2023},
  journal = {EFSA Journal},
  volume = {21},
  number = {7},
  pages = {8164},
  doi = {10.2903/j.efsa.2023.8164},
  tier = {1},
  klimisch = {n/a},
  glp = {n/a},
  guideline = {EFSA peer review},
  coi = {REG},
  accessed = {2026-05-29}
}

@misc{reg1107_2009,
  author = {{European Commission}},
  title = {Regulation (EC) No 1107/2009 concerning the placing of plant protection products on the market},
  year = {2009},
  howpublished = {OJ L 309, 24.11.2009, p. 1-50},
  note = {CELEX:32009R1107},
  tier = {1},
  accessed = {2026-05-29}
}
```

## Citation verification

Every citation in `REVIEW.md` must:
1. Resolve to a live DOI, CELEX, or URL
2. Match author/year/title/journal as printed at the source
3. Support the specific claim made in the cited sentence (verify by retrieving the source text)
4. Carry tier and (if Tier 3) Klimisch + GLP + guideline flags in `BIBLIOGRAPHY.bib`

Log every verified citation in `CITATION-LEDGER.md` per the SKILL.md Phase 7 specification.
