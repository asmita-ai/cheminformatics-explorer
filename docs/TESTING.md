# Test Results & Validation Summary

**Project:** Cheminformatics Explorer v1.0.0  
**Author:** Asmita Karmakar ([ORCID 0009-0004-4710-5237](https://orcid.org/0009-0004-4710-5237))  
**Date:** October 15, 2026  
**Status:** ALL ACCEPTANCE CRITERIA PASSED

---

## 1. Scope of Validation

The application underwent rigorous automated testing across five planned engineering phases using headless Google Chrome and Puppeteer Core on Windows.

### Test Categories
1. **Chemical Identifier Resolution:** Compound names, formulas with and without digits, direct PubChem CIDs, and canonical SMILES strings.
2. **Computational Engines:** RDKit.js MinimalLib WASM (2D vector depictions, SMARTS substructure pattern matching, Wildman-Crippen logP, PAINS/Brenk alerts) and 3Dmol.js (WebGL conformer rendering).
3. **External Data Provenance:** PubChem PUG REST/View, NCI Chemical Identifier Resolver, ChEBI ontology trees, and ChEMBL bioactivity links.
4. **Learning Layer:** Student vs. Researcher mode toggling across all tabs with zero page reloads.
5. **Responsiveness & Accessibility:** 360 px mobile viewport compliance (zero horizontal scroll) and Axe-Core / Lighthouse accessibility audit.
6. **Network & Client Optimization:** Request queue rate limiting ($\le 3$ req/sec), 24-hour `sessionStorage` caching, on-demand lazy tab data fetching, and friendly retry backoff on HTTP 429/503.

---

## 2. Chemical Input Verification Matrix

All 15 required chemical test inputs resolved properly without uncaught exceptions:

| Test Query | Type | Expected Behavior | Observed Result | Status |
|---|---|---|---|---|
| `caffeine` | Common name | Resolves CID 2519, renders 3D conformer & 2D structure | Loaded conformer, MW 194.19, XLogP3 -0.07 | **PASS** |
| `aspirin` | Common name | Resolves CID 2244, highlights Carboxylic Acid & Ester | Loaded conformer, detected 2 functional groups | **PASS** |
| `ibuprofen` | Common name | Resolves CID 3672, highlights Carboxylic Acid | Loaded conformer, MW 206.28, 0 Lipinski violations | **PASS** |
| `atorvastatin` | Common name | Resolves CID 60823, flags 1 Lipinski rule violation | MW 558.6 Da flagged (MW > 500 criterion) | **PASS** |
| `penicillin G` | Common name | Resolves CID 5904, Beta-lactam / Amide matching | Loaded conformer, GHS Danger signal word parsed | **PASS** |
| `glucose` | Common name | Resolves CID 5793, Alcohol functional groups highlighted | Loaded conformer, 5 Alcohol groups detected | **PASS** |
| `benzene` | Common name | Resolves CID 241, planar aromatic ring rendered | Planar 3D conformer, aromatic SMARTS match | **PASS** |
| `C6H6` | Molecular formula | Resolves via `fastformula` to Benzene | Correctly routed to CID 241 with isomer note | **PASS** |
| `C8H10N4O2` | Molecular formula | Resolves via `fastformula` to Caffeine | Correctly routed to CID 2519 with isomer note | **PASS** |
| `sodium chloride` | Ionic salt | Honest 2D fallback (no theoretical 3D record) | Correctly labeled "2D Layout (no 3D record)" | **PASS** |
| `mercury` | Elemental metal | Single-atom coordinate fallback | Correctly handled with element-level metadata | **PASS** |
| `"water"` | Quoted name | Strips quotes, resolves CID 962 | Rendered bent geometry, MW 18.015 g/mol | **PASS** |
| `gibberishxyz123` | Invalid query | Human-readable compound not found notice | Rendered helpful "No PubChem match" alert | **PASS** |
| `""` (Empty string) | Empty query | Friendly guidance message | Rendered "Empty Search Input" prompt | **PASS** |
| Long string (>150 chars) | Input boundary | Prevents buffer overrun / long queries | Rendered "Query Too Long" notice | **PASS** |

---

## 3. Accessibility & Performance Benchmarks

- **Axe-Core / Lighthouse Accessibility:** Audited across WCAG 2.1 Level AA rules; passed **43 out of 43 audit checks with 0 violations** (Score: **100%**).
- **Mobile Viewport (360 px):** Verified `scrollWidth === clientWidth === 360` with zero horizontal scrolling. 3D viewer stacks cleanly above tabs.
- **Network Request Footprint:** Initial search for caffeine executes strictly **5 requests** (CID resolution, properties, 3D SDF conformer, synonyms, and record description), well below the $\le 6$ request limit.
- **Uncaught Page Exceptions:** **0** across all automated test runs.
- **GHS Consensus Validation:** Verified non-merging reference grouping with ECHA C&L consensus headlines, notification percentages, and minority supplier cards across Caffeine (Warning, H302 only, Acute Tox. 4 98.9%), Aspirin, Ibuprofen, Benzene, Glucose, and Water.
