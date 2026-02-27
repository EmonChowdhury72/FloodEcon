# FloodEcon: Mapping the Economic Footprint of Climate Disasters

> Transforming flood imagery into concrete economic evidence, one classification at a time.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Solution](#solution)
- [How It Works](#how-it-works)
- [Workflow Design](#workflow-design)
- [Technology Stack](#technology-stack)
- [Implementation Roadmap](#implementation-roadmap)
- [Impact and Objectives](#impact-and-objectives)
- [SDG Alignment](#sdg-alignment)
- [Data and File Structure](#data-and-file-structure)
- [Monitoring and Evaluation](#monitoring-and-evaluation)
- [Risk Analysis](#risk-analysis)
- [Legal and Ethics](#legal-and-ethics)
- [Future Roadmap](#future-roadmap)
- [Key Economic Data](#key-economic-data)
- [References](#references)
- [License](#license)

---

## Project Overview

**FloodEcon** is a citizen science research project that mobilizes global volunteers to classify pre- and post-flood satellite imagery of Bangladeshi flood zones. Volunteers examine Sentinel-1 and Sentinel-2 satellite image pairs and complete three structured classification tasks: pre-flood land-use identification, post-flood damage severity marking, and economic sector classification.

The aggregated human classifications produce a granular, open-access economic damage dataset at a spatial resolution and speed that traditional assessment methods cannot match.

**Project Type:** Citizen Science Research Platform and Data Infrastructure Initiative  
**Platform:** Zooniverse  
**Zooniverse Project:** https://www.zooniverse.org/projects/emonchowdhury/floodecon-mapping-the-economic-footprint-of-climate-disasters  
**Status:** Ideation, Pre-Planning  
**Target Launch:** August 2026

---

## Problem Statement

Bangladesh is ranked the 7th most climate-vulnerable nation globally and faces catastrophic flooding nearly every monsoon season. The August-September 2024 floods inundated 11 districts, killed hundreds, displaced millions, and caused approximately US $1.676 billion in direct economic damage.

Despite the scale of these events, post-disaster economic assessments remain slow, expensive, expert-dependent, and institutionally fragmented. This creates three compounding failures:

- Assessments arrive too late to inform emergency policy decisions
- National-level damage estimates mask sector-by-sector and district-by-district variation
- Self-reported government damage figures lack independent scientific verification, which is a direct barrier to accessing international climate finance such as the COP28 Loss and Damage Fund

**Why current solutions fall short:**

| Approach | Limitation |
|---|---|
| Government damage surveys | Takes weeks to months; methodologically inconsistent across agencies |
| Automated AI mapping | Detects physical damage well but cannot classify economic sector without labeled training data |
| Expert platforms (UNOSAT, Copernicus EMS) | Produces physical damage maps only; no economic sector dimension |
| Existing Zooniverse climate projects | Address physical or historical climate phenomena; none quantify economic impact |

---

## Solution

FloodEcon deploys the Zooniverse Project Builder to create a structured, three-task classification workflow. Global volunteers examine side-by-side pre-flood and post-flood satellite imagery tiles and answer three questions:

1. **What was here before?** (Pre-flood land use)
2. **What happened to it?** (Damage severity)
3. **What economic sector does it belong to?** (Economic classification)

Each image tile is independently reviewed by 15 to 20 volunteers. Classifications are aggregated via the Zooniverse Caesar engine using weighted voting, producing statistically robust economic sector damage records at the tile level.

**Why FloodEcon is better:**

| Criterion | Traditional Survey | Automated AI Mapping | FloodEcon |
|---|---|---|---|
| Speed | Weeks to months | Hours to days | Days |
| Cost | High (field teams) | Medium (commercial tools) | Near-zero (volunteers and free imagery) |
| Economic sector detail | Yes, but slow | No | Yes |
| Spatial granularity | Low to medium | High (physical only) | High (economic) |
| Open access | Rarely | Rarely | Always |
| ML training data generated | No | No | Yes |
| Global volunteer engagement | No | No | Yes |

---

## How It Works

```
SATELLITE DATA PIPELINE

Sentinel-1 (SAR, cloud-piercing) + Sentinel-2 (optical, 10m resolution)
         |
         v
Preprocessed in Google Earth Engine (NDWI, band composites, cloud masking)
         |
         v
Image Tiles (~256x256m) exported and uploaded to Zooniverse Subject Sets
         |
         v
VOLUNTEER CLASSIFICATION WORKFLOW

  Task 1 --> Pre-flood land use classification
  Task 2 --> Post-flood damage severity marking (point labels)
  Task 3 --> Economic sector classification

         |
         v
Caesar Aggregation Engine (15-20 classifications per tile, weighted voting)
         |
         v
ECONOMIC DAMAGE DATASET

  GeoJSON + CSV --> Open-access repository (Zenodo, GitHub)
         |
         v
ML TRAINING PIPELINE

  Human labels --> CNN / Random Forest damage detection model
         |
         v
RESEARCH AND POLICY OUTPUTS

  Peer-reviewed paper + Policy brief + Loss and Damage Fund data
```

---

## Workflow Design

### Workflow 1: Pre-Flood Land Use

- **Subject type:** Single pre-flood Sentinel-2 true-color image
- **Task:** Multiple-choice question: "What type of land use is visible in this image?"
- **Options:** Residential, Agricultural, Commercial or Market, Industrial, Infrastructure, Forest, Water, Mixed, Unclear
- **Tool:** Question Task (single answer)

### Workflow 2: Flood Damage Severity

- **Subject type:** Side-by-side image pair (pre-flood and post-flood)
- **Task A:** "Is flooding or flood damage visible in the post-flood image?" (Yes / No / Uncertain)
- **Task B (if Yes):** "Mark the center of each damaged or flooded structure or area" (Point marking tool)
- **Task C:** "Rate the overall damage severity" (None / Mild / Moderate / Severe / Catastrophic)
- **Tool:** Point Marking Task and Question Task

### Workflow 3: Economic Sector Classification

- **Subject type:** Same image pair from Workflow 2 (routed only if damage is confirmed)
- **Task:** "Based on visible structures and land use, what is the primary economic activity of this damaged area?"
- **Options:** Food Production or Farming, Retail or Market or Commerce, Manufacturing or Industry, Transport or Logistics, Public Infrastructure, Residential Livelihood, Mixed Economic, Cannot Determine
- **Tool:** Question Task with optional short text field

---

## Technology Stack

| Layer | Tools | Cost |
|---|---|---|
| Satellite Data | Sentinel-1 and Sentinel-2 (ESA Copernicus) | Free |
| Cloud Processing | Google Earth Engine (research license) | Free |
| GIS | QGIS, GDAL, rasterio | Free / Open Source |
| Platform | Zooniverse Project Builder and Panoptes API | Free |
| Aggregation Engine | Caesar (Zooniverse) | Free |
| ML and Analysis | Python (scikit-learn, TensorFlow), R | Free |
| Visualization | Kepler.gl, Power BI | Free / Low cost |
| Data Repository | Zenodo (CERN), GitHub | Free |
| Communication and Branding | Canva Pro, WordPress | ~$50 one-time |

---

## Implementation Roadmap

### Phase 1: Research and Scoping (March - April 2026)

**Goal:** Establish scientific foundation, define spatial scope, acquire satellite data, and design classification schema.

Key deliverables:
- Literature review on satellite flood mapping methods
- Sentinel-1 and Sentinel-2 tiles downloaded for 11 districts (August 2024 event)
- 50 preprocessed image tile pairs as proof of concept
- Finalized classification label ontology for all three workflows

**Milestone:** 50 validated image tile pairs and finalized classification schema

---

### Phase 2: Design and Project Build (May - June 2026)

**Goal:** Build the Zooniverse project, design all three workflows, and write research documentation.

Key deliverables:
- Zooniverse project shell created in Project Builder
- All three workflows built and tested
- Volunteer tutorial and field guide written for each workflow
- First 50 subject image pairs uploaded
- Internal testing completed with 5 to 10 testers

**Milestone:** Functional Zooniverse project (private/beta) with 3 workflows and 50 subject pairs tested

---

### Phase 3: Beta Review and Launch (July - August 2026)

**Goal:** Submit to Zooniverse official review, complete beta testing, and publicly launch.

Key deliverables:
- Project submitted for Zooniverse Internal Review
- Beta test completed with Zooniverse volunteer testers
- Inter-volunteer agreement (IAA) analyzed for workflow clarity
- Full dataset of 500 image pairs uploaded across 11 districts
- Social media and press release campaign executed on launch day

**Milestone:** Official Zooniverse launch with 500 image pairs and 2,000+ classifications in the first two weeks

---

### Phase 4: Active Research and Data Collection (September - December 2026)

**Goal:** Achieve target classification volume, run spatial analysis, and produce research outputs.

Key deliverables:
- Weekly monitoring of classification volume
- Volunteer community engagement on Talk boards
- Spatial join of classification data to administrative district boundaries
- District-level economic damage maps produced for 8 of 11 districts
- Draft Research Paper 1 and Policy Brief 1 completed

**Milestone:** Full economic damage dataset for 8 districts and draft paper submitted to journal

---

### Phase 5: Scale and Replication (2027)

**Goal:** Publish, present, expand geographically, and establish FloodEcon as a replicable methodology.

Key deliverables:
- Research paper submitted to target journal
- Open-access dataset published on Zenodo
- Pilot replication in one new country (Nepal or Myanmar)
- Open-source FloodEcon methodology toolkit released on GitHub
- Grant applications submitted for Phase 3 geographic expansion

**Milestone:** Published paper, open-access dataset, methodology toolkit, and one international replication

---

### Timeline Summary

```
2026
Mar  Apr  May  Jun  Jul  Aug  Sep  Oct  Nov  Dec
|---------|   |---------|   |---------|   |------------------------|
 Phase 1        Phase 2        Phase 3         Phase 4 (Active)

2027
Jan  Feb  Mar  Apr  May  Jun  Jul  Aug  Sep
|-----------------------------------------------|
            Phase 5 (Scale and Publication)
```

---

## Impact and Objectives

### Strategic Objectives

| Objective | Timeframe |
|---|---|
| Launch a functional Zooniverse project with 3 workflow tasks processing a minimum of 1,000 satellite image pairs from the 2024 Bangladesh floods | Q2 2026 |
| Achieve 500+ volunteer classifications per subject and generate a publication-grade economic damage dataset for at least 5 districts in eastern Bangladesh | Q3-Q4 2026 |
| Publish one peer-reviewed paper and one policy brief linking FloodEcon data to Loss and Damage Fund access mechanisms, and pilot replication in one additional South Asian country | Q1 2027 |

### Success Definitions

- 10,000+ volunteer classifications in the first 3 months post-launch
- Economic sector damage data covering 8 or more of the 11 affected districts
- At least 1 accepted peer-reviewed publication in a Q1/Q2 journal
- Project cited in at least one UNDP, World Bank, or government policy document related to Bangladesh climate finance
- 85%+ inter-volunteer agreement rate (IAA) on classification tasks validated against expert-labeled ground truth

### Key Performance Indicators

| KPI | Target | Frequency |
|---|---|---|
| Total volunteer classifications | 10,000 (Month 1), 50,000 (Month 3), 250,000 (Year 1) | Weekly |
| Inter-volunteer agreement rate (IAA) | 85% per workflow | Monthly |
| Subject retirement rate | 90%+ within 60 days of launch | Monthly |
| Geographic coverage | 11 of 11 districts with 100+ classified tiles | Quarterly |
| Classification accuracy vs. ground truth | 80%+ accuracy | Phase 4 (once) |
| Peer-reviewed publications submitted | 1 draft by December 2026 | Quarterly |

---

## SDG Alignment

| SDG | Target | How FloodEcon Contributes |
|---|---|---|
| SDG 1 (No Poverty) | 1.5: Reduce economic losses from disasters | Provides sector-level damage data for recovery targeting |
| SDG 11 (Sustainable Cities) | 11.5: Reduce economic losses from disasters | Granular urban damage classification supports resilient rebuilding |
| SDG 13 (Climate Action) | 13.1: Strengthen resilience to climate hazards | Generates a scientific basis for Loss and Damage Fund access |
| SDG 17 (Partnerships) | 17.6: Knowledge-sharing partnerships | Open-access data and global volunteer collaboration |

FloodEcon directly produces data aligned with the Sendai Framework for Disaster Risk Reduction (2015-2030), which calls for the "proportion of total cost of damages and direct economic loss due to disasters to GDP" as a core indicator.

---

## Data and File Structure

```
FloodEcon/
|-- 01_Data/
|   |-- Raw_Imagery/            # Downloaded Sentinel tiles
|   |-- Processed_Tiles/        # GEE-processed image pairs
|   |-- Ground_Truth/           # CPD, World Bank, FAO reports
|
|-- 02_GEE_Scripts/             # Google Earth Engine processing code
|
|-- 03_Zooniverse/
|   |-- Subject_Sets/           # Uploaded image tiles
|   |-- Classification_Exports/ # Caesar CSV exports
|   |-- Workflow_Design/        # Workflow screenshots, logic diagrams
|
|-- 04_Analysis/
|   |-- Python_Scripts/         # Classification aggregation, spatial join
|   |-- R_Scripts/              # Statistical analysis
|
|-- 05_Outputs/
|   |-- Datasets/               # Final GeoJSON + CSV damage datasets
|   |-- Maps/                   # QGIS output maps
|   |-- Publications/           # Draft papers, policy briefs
|
|-- 06_Admin/
|   |-- Grants/                 # Grant applications
|   |-- Partnerships/           # MOU templates, partner contacts
|
|-- README.md                   # Project overview and onboarding guide
```

### Version Control Conventions

- All code, GEE scripts, and analysis notebooks are maintained under MIT License
- Git commit prefixes: `feat:`, `fix:`, `data:`, `docs:`
- Dataset releases are tagged as `v1.0`, `v1.1`, etc., with changelogs

### Data Storage

- Working data: Google Drive (access-controlled)
- Published data: Zenodo (CERN DOI-minted, permanent, citable)
- Imagery backups: Local hard drive with cloud redundancy

---

## Monitoring and Evaluation

### Evaluation Schedule

| Period | Evaluation Type | Output |
|---|---|---|
| End of Beta Test (August 2026) | Formative: workflow design quality | Workflow revision report |
| Month 3 post-launch (November 2026) | Progress: classification volume and IAA | Internal progress brief |
| End of Phase 4 (December 2026) | Summative: data quality and coverage | Research paper draft |
| End of Phase 5 (December 2027) | Impact: citations, replications, policy uptake | Annual impact report |

### Data Collection Methods

- Zooniverse analytics dashboard for real-time classification tracking
- Caesar export API for aggregated classification data in CSV/JSON
- GitHub commit logs for development progress
- Expert validation survey sent to 3-5 remote sensing experts

---

## Risk Analysis

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| Zooniverse review rejection or delay | Low | High | Build project to highest standards; follow lab policies; engage Zooniverse team early |
| Low volunteer engagement | Medium | High | Leverage Zooniverse newsletter; promote via LinkedIn, academic networks, and science communities |
| Poor image quality due to cloud cover | High | Medium | Use Sentinel-1 SAR as primary (cloud-piercing); supplement with Sentinel-2 where cloud-free |
| Low inter-volunteer agreement (IAA below 80%) | Medium | High | Invest in tutorial design and example images; simplify early workflows |
| CPD ground truth data inaccessible | Low | Medium | Use World Bank GRADE and FAO DIEM reports as backup validation |
| Platform deprecation | Very Low | Very High | Maintain independent backup of all subject images and classification data on Zenodo and GitHub |
| ML model underperforms on labeled dataset | Medium | Low | Human classifications remain the primary output regardless of ML performance |
| Data privacy concerns | Low | Medium | Use Sentinel medium-resolution imagery (10m/px); no individual identification is possible at this resolution |

---

## Legal and Ethics

### Data Privacy

- All satellite imagery is publicly licensed under the Copernicus Open Licence (free use for any purpose, including commercial)
- Sentinel imagery resolution is 10m per pixel, meaning no individual identification is possible
- No personal data of disaster-affected individuals is collected or processed
- Volunteer accounts are managed entirely by Zooniverse, which is GDPR-compliant

### Ethical Considerations

- **Representation:** FloodEcon classifies damage affecting communities not directly involved in the research. The project partners with Bangladeshi institutions (CPD, BRAC) to ensure community interests are represented in research design and outputs
- **Data use:** All data is released under Creative Commons CC-BY 4.0, ensuring broad access including by affected communities
- **Sensitivity:** Tutorial language will be reviewed for appropriate tone; imagery of damaged areas is framed as scientific data, not disaster spectacle
- **Credit:** All volunteer contributions are acknowledged per Zooniverse standard practice

### Licensing

| Asset | License |
|---|---|
| Satellite imagery | ESA Copernicus Open Licence |
| Generated dataset | Creative Commons CC-BY 4.0 |
| Source code and scripts | MIT License |
| Research publications | Open-access journals (target: no APC barrier) |

---

## Future Roadmap

| Version | Scope | Target |
|---|---|---|
| v1.0 FloodEcon Bangladesh | 2024 flood events, 11 districts, 1,000 image pairs | August 2026 |
| v1.1 Temporal Expansion | Add 2022 and 2023 Bangladesh flood events for longitudinal analysis | Q4 2026 |
| v2.0 FloodEcon South Asia | Nepal and Myanmar pilot (monsoon flood contexts) | Q2 2027 |
| v2.5 Near Real-Time Mode | Integrate Copernicus Emergency Management Service API for rapid post-disaster deployment | Q3 2027 |
| v3.0 FloodEcon Global South | Sub-Saharan Africa, Central America | 2028 |
| v4.0 FloodEcon Platform | Standalone platform enabling any research team to deploy the FloodEcon methodology independently | 2029+ |

### Planned Features

- Drag-and-drop temporal slider for before/after image comparison
- Mobile-first classification interface
- Field photo integration from local community members matched to satellite tiles
- Economic exposure model using OSM building footprints to prioritize high-value tiles for human review
- Bengali, Arabic, and French interface translations for regional volunteer communities

### Target Scaling Regions

| Region | Rationale |
|---|---|
| Nepal | Annual Terai lowland flooding; limited damage assessment capacity |
| Mozambique | Cyclone-induced flooding; existing UN-SPIDER Sentinel use cases |
| Nigeria | Benue and Niger River flooding; large population exposure |
| Pakistan | Indus River flooding, precedent from 2022 mega-flood |

---

## Key Economic Data

### Bangladesh 2024 Flood Damage by Sector

| Sector | Damage (Tk crore) | Percentage of Total | USD Equivalent |
|---|---|---|---|
| Agriculture and Forestry | 5,169.71 | 35.85% | ~$430M |
| Infrastructure | 4,653.92 | 32.27% | ~$388M |
| Housing | 2,407.31 | 16.69% | ~$200M |
| Other (livelihoods, health, education) | 2,190.52 | 15.19% | ~$183M |
| **Total** | **14,421.46** | **100%** | **~$1.20B** |

*Source: Centre for Policy Dialogue (CPD), October 2024*

World Bank GRADE independent estimate: **US $1.676 billion** (median direct economic damage)

---

## References

| Reference | Relevance |
|---|---|
| Kuzin et al. (2021), "Disaster mapping from satellites: damage detection with crowdsourced point labels," arXiv:2111.03693 | Core methodology precedent for point-label crowdsourcing |
| World Bank GRADE Report (2024), "Floods in Eastern Bangladesh, August 2024" | Primary ground truth for damage validation |
| Khatun, F. et al. (2025), "Eastern Bangladesh Floods in 2024: Analysis of Immediate Economic Impact," CPD Policy Brief | Sector-level ground truth for classification schema |
| FAO DIEM Impact Report (2024), "Bangladesh: Impact of the Floods on Agricultural Livelihoods" | Agricultural sector damage validation |
| Lintott et al. (2008), "Galaxy Zoo: Morphologies Derived from Visual Inspection of Galaxies from the SDSS" | Foundational Zooniverse accuracy and aggregation methodology |
| Naumann, G. et al. (2019), "Citizen Science and Crowdsourcing for Flood Mapping," Frontiers in Earth Science | Crowdsourced flood science methodology review |
| "Crowdsourcing Intelligence for Disaster Forecasting," PMC (2024) | Framework for human-AI hybrid disaster modeling |
| UN-SPIDER (2025), "Flood Mapping Using Sentinel-1 and Sentinel-2" | Validated satellite imagery workflow |

### Data Sources

| Dataset | Source | Access |
|---|---|---|
| Sentinel-1 SAR flood imagery | ESA Copernicus Open Access Hub | Free |
| Sentinel-2 optical imagery | ESA Copernicus Open Access Hub | Free |
| 2024 Bangladesh flood damage records | CPD, World Bank GRADE, FAO DIEM | Public reports |
| Bangladesh district shapefiles | GADM and Bangladesh BBS | Free |
| SPARRSO flood inundation maps | Bangladesh SPARRSO | Request-based |

---

## License

- **Code:** MIT License
- **Dataset:** Creative Commons CC-BY 4.0
- **Satellite Imagery:** ESA Copernicus Open Licence

---

*FloodEcon is an open research initiative. Contributions, collaborations, and replications are welcome. See the Issues tab to discuss ideas or report problems.*
