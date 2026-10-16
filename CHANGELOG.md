# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-10-15

### Added
- **Interactive 3D Molecular Viewer:** Hardware-accelerated WebGL conformer rendering via 3Dmol.js with Ball & Stick, Sticks, and Spheres representation styles and spin controls.
- **RDKit.js WASM 2D Depiction & SMARTS Matching:** Clean SVG chemical depictions with interactive functional group substructure highlights.
- **Dual-Audience Learning Layer:** Dynamic "Student" and "Researcher" modes explaining concepts in plain language or formal mathematical descriptors without page reloads.
- **Oral Drug-Likeness Evaluation:** Quantitative Lipinski Rule of 5 and Veber bioavailability screening with Crippen logP vs XLogP3-AA comparisons.
- **Medicinal Chemistry Structural Alerts:** PAINS (Pan-Assay Interference Compounds) and Brenk reactive functional group filter catalog matching.
- **Chemical Structure Sketcher & SMILES Resolver:** Integrated 2D JSME canvas drawer and direct chemical SMILES query resolution.
- **GHS Safety & Hazard Classifications:** Aggregated chemical manufacturer GHS hazard pictograms, signal words, and laboratory PPE guidance.
- **2D Similarity Exploration:** PubChem `fastsimilarity_2d` Tanimoto $\ge 85\%$ search with 2D vector thumbnails.
- **Experimental Physical Properties & Biological Roles:** PUG View experimental melting point, boiling point, solubility, density with source citations, ChEBI biological ontology roles, and ChEMBL clinical trial links.
- **Methods Citation Copy:** One-click academic bibliography generator.
- **Accessible Design:** 100% Axe-Core accessibility compliance, keyboard focus rings, ARIA landmarks, and 360 px zero-horizontal-scroll layout.
- **Consensus GHS Safety Classification:** Resolved primary regulatory headlines (ECHA C&L aggregate) with notification percentages and separated minority supplier cards instead of merging worst-case hazards.
- **Client-Side Request Optimization:** 3 req/sec rate limiter with exponential backoff on HTTP 429/503, 24-hour `sessionStorage` caching, and on-demand lazy tab data fetching.
