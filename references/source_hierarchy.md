# Source Hierarchy for PPP Literature Review

Sources are weighted by regulatory defensibility, not novelty or impact factor. The order below governs conflict resolution: when sources disagree on a quantitative endpoint or regulatory position, the higher-tier source prevails unless the lower-tier source post-dates it and presents new primary data.

## Tier 1 - Regulatory primary (highest weight)

| Source | Authority | Citation form | Notes |
|---|---|---|---|
| EFSA Conclusion on the peer review | EFSA + RMS + MS experts | EFSA Journal YYYY;VV(N):NNNN | Canonical EU position on active substance |
| EFSA Scientific Opinion (PPR, FEEDAP, etc.) | EFSA Panel | EFSA Journal YYYY;VV(N):NNNN | Methodology, cross-cutting issues |
| EFSA Reasoned Opinion on MRLs | EFSA | EFSA Journal YYYY;VV(N):NNNN | MRL setting / Article 12 |
| EFSA Guidance Document | EFSA | EFSA Journal YYYY | Methodological authority |
| ECHA RAC Opinion (CLH) | ECHA Risk Assessment Committee | ECHA/RAC/CLH-O-XXXX | Harmonised classification |
| ECHA REACH registration dossier | ECHA | echa.europa.eu dossier ID | Co-formulant / substance data |
| Renewal Assessment Report (RAR) | RMS | RMS, Vol. N, YYYY | EU renewal evidence base |
| Draft Assessment Report (DAR) | RMS | RMS, Vol. N, YYYY | Initial EU evaluation |
| EU Pesticides Database | EU Commission | ec.europa.eu/food/plant/pesticides/eu-pesticides-database | Live status |
| Codex Alimentarius MRL | Codex | Codex Alimentarius CXP MMM | International MRL reference |
| JMPR / JECFA monograph | FAO/WHO | JMPR YYYY, FAO Plant Production and Protection Paper | International tox reference |
| OECD Test Guideline | OECD | OECD TG NNN, year of adoption | Methodological gold standard |
| OECD Series on Testing and Assessment | OECD | OECD ENV/JM/MONO(YYYY)N | Methodological |
| EU legislation | Council / Parliament | CELEX:32YYYRNNNN, Art. N | Cite consolidated text plus most recent amendment |

## Tier 2 - Authoritative secondary

| Source | Authority | Notes |
|---|---|---|
| US EPA OPP risk assessment / RED | US EPA | Cross-jurisdictional comparator |
| PMRA Re-evaluation Decision | Health Canada PMRA | |
| APVMA review | Australia APVMA | |
| IARC Monograph | IARC | Carcinogen classification |
| NTP Report on Carcinogens | US NTP | |
| WHO/IPCS Environmental Health Criteria | WHO | |
| IUCLID / eChemPortal extract | ECHA / OECD | |
| BCPC Pesticide Manual | BCPC | Identity, mode of action |
| PPDB (Hertfordshire) | University of Hertfordshire | Aggregated endpoint values; verify against primary source |
| BPDB (Hertfordshire) | University of Hertfordshire | Biopesticides equivalent |

## Tier 3 - Peer-reviewed primary literature

Priority journals (non-exhaustive, ordered by typical regulatory relevance):

- Journal of Agricultural and Food Chemistry
- Pest Management Science
- Environmental Toxicology and Chemistry
- Chemosphere
- Science of the Total Environment
- Regulatory Toxicology and Pharmacology
- Critical Reviews in Toxicology
- Food and Chemical Toxicology
- Archives of Toxicology
- EFSA Journal (also Tier 1 for opinions/conclusions)
- Environmental Science and Technology
- Ecotoxicology and Environmental Safety
- Aquatic Toxicology
- Environmental Pollution
- Journal of Hazardous Materials
- Toxicological Sciences
- Reproductive Toxicology
- Mutation Research
- Crop Protection
- Weed Research / Weed Science

Klimisch 1 GLP studies in priority journals are the strongest Tier 3 evidence. Non-GLP studies require explicit Klimisch justification.

## Tier 4 - Grey literature (always flag tier in citation)

| Source | Use | Caveat |
|---|---|---|
| ECPA / CropLife task force reports | Mode of action, cumulative assessment groups | Industry-sponsored; flag COI |
| SETAC / BCPC Congress proceedings | Methodological updates | Often pre-publication |
| University theses | Mechanistic detail | Cite only if used by Tier 1-3 |
| Preprints (bioRxiv, ChemRxiv, EarthArXiv) | Latest findings | Verify subsequent peer review status |
| Trade press (Agrow, AgriBusiness Global) | Market and policy context | Not for scientific claims |

## Default rejections

Do not cite:
- Predatory journals (cross-check Beall's list legacy + Cabells Predatory Reports)
- Non-English sources without verified translation provenance
- Advocacy NGO claims unless triangulated against Tier 1-2 primary data
- Wikipedia, blogs, social media
- Press releases as scientific evidence (cite the underlying study instead)

## Conflict resolution algorithm

1. If both sources Tier 1-2: prefer the more recent unless the older is the EFSA conclusion-of-record and no renewal has superseded it.
2. If Tier 1-2 vs Tier 3: Tier 1-2 prevails unless Tier 3 post-dates AND introduces new primary data not assessed in the Tier 1-2 source.
3. If Tier 3 vs Tier 3: Klimisch 1 GLP guideline-compliant prevails over non-GLP.
4. If conflict persists: present both; weight by evidence; explicit hedging; recommend further data.

Document every conflict resolution in the review body.

## COI flag taxonomy

| Code | Meaning |
|---|---|
| IND-NOTIFIED | Industry-funded, applicant-notified |
| IND-OTHER | Industry-funded, other manufacturer |
| TF | Task-force consortium |
| REG | Regulatory authority funded |
| ACAD-PUB | Academic, public funding |
| ACAD-MIX | Academic, mixed public/industry |
| NGO | NGO-funded |
| UND | Undisclosed funding |

COI does not invalidate a study but does affect weight under EFSA WoE guidance.
