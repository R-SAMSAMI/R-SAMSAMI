# Reihaneh (Rei) Samsami

**I build AI systems for construction and infrastructure: inspection copilots, document intelligence, and BIM data pipelines that survive contact with real field data.**

Most AI in this industry breaks on the same thing. The inputs are site photos, scanned spec books, agency standards, and Revit schedule exports that were never meant to be machine-readable, and the outputs get handed to an inspector or a superintendent who is accountable for them. I work on the layers in between: extraction, grounding, structured output, and the evaluation that has to exist before any of it is safe to ship.

Ph.D. Civil Engineering · M.S. Data Science · Licensed PE  
Co-PI, **NCHRP 10-110A** (Transportation Research Board, 2025–present) · previously **MDOT UAV III**  
Assistant Professor, University of New Haven

**Open to AI engineering roles building products for construction, infrastructure, and the built environment.**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Reihaneh%20Samsami-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rsamsami)
[![Google Scholar](https://img.shields.io/badge/Google%20Scholar-Publications-4285F4?style=for-the-badge&logo=googlescholar&logoColor=white)](https://scholar.google.com/citations?user=6AyoxZ0AAAAJ&hl=en&oi=ao)
[![Email](https://img.shields.io/badge/Email-rsamsami%40newhaven.edu-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:rsamsami@newhaven.edu)

---

## Featured Work

### Does Grounding Matter? LLMs vs. Agency Inspection Standards
**[`inspection-llm-grounding`](https://github.com/R-SAMSAMI/inspection-llm-grounding)** · Submitted to TRB 2027

A controlled benchmark isolating what closed-book, RAG, and full-document grounding actually do for construction inspection Q&A. Built because the industry is shipping LLM features against agency specs with no measurement of whether the answers are defensible.

**Design:** 3 frontier LLMs × 70 validated inspection questions × 3 grounding conditions = **600 scored responses** (~630 API calls, fully reproducible via Colab).

| Finding | Result |
| --- | --- |
| Ungrounded answers rated factually unacceptable | **56–64%** across all three models |
| Composite score lift from grounding | **+1.3 to +1.7 points** per model (p < 0.000001) |
| Full-document vs. RAG | **+0.14 average, at ~35× the input tokens** |
| Expert validation of the automated scoring | **Spearman 0.77**, 82.7% within one point |

**So what:** closed-book LLMs are not usable for specification questions. RAG is the correct default at agency document scale, and the full-context premium is not worth 35× the token spend except on project-specific contractual documents.

**Corpus:** public CTDOT, OSHA, and FHWA publications. Code MIT, data and results CC BY 4.0.
`Python · RAG · LLM evaluation · Claude / GPT / Gemini APIs · statistical validation`

---

### BIMOps AI: Revit to Databricks Lakehouse
**[`bimops-ai`](https://github.com/R-SAMSAMI/bimops-ai)**

An end-to-end medallion pipeline turning Revit schedule exports into governed, queryable analytics, plus a natural-language query layer over the Gold tables.

**Scale:** 17 Revit schedule exports across architectural, electrical, mechanical, and structural disciplines, roughly **5,500 BIM records** through Bronze → Silver → Gold.

- **BIM readiness scoring** that quantifies metadata completeness (`1 − missing important values / total important values`), so model quality becomes a number a project team can act on instead of an opinion
- Cross-discipline program analytics, asset inventories, and life-safety rollups
- Data dictionaries, governance framework, and RBAC-aware access design
- Streamlit Databricks App for conversational exploration of the governed tables

`Databricks · Delta Lake · SQL · PySpark · Python · Revit · Power BI`

---

### Agentic Construction Safety Copilot
**[`agentic-construction-safety-copilot`](https://github.com/R-SAMSAMI/agentic-construction-safety-copilot)** · [![Live demo](https://img.shields.io/badge/Live%20demo-open-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://rei-safety-copilot.streamlit.app/)

A multimodal safety review workspace that turns field observations and site photos into structured signals, risk posture, OSHA-style control-gap findings, corrective actions, and a toolbox-talk brief. Built as a workflow product, not a prompt wrapper.

- **Pydantic-enforced structured outputs** end to end, so every field in the report is schema-validated before it reaches a supervisor
- Scenario library across **5 project types**: concrete, steel, civil/bridge, roofing/envelope, MEP/interiors
- Dual execution modes: a deterministic offline mode for reproducible demos and regression checks, and a live multimodal mode against the OpenAI Responses API
- Explicit uncertainty handling and human-in-the-loop positioning; the tool drafts, the competent person decides

Concept direction inspired by [Sharmin Jahan Badhan](https://github.com/sharmin3036); productization and implementation mine.

`Python · OpenAI Responses API · Pydantic · Streamlit · multimodal AI`

---

## More Projects

### Copilots and document AI

| Project | What it demonstrates | Stack |
| --- | --- | --- |
| [Construction Docs Copilot](https://github.com/R-SAMSAMI/construction-docs-copilot) · **[live demo](https://rei-docs-copilot.streamlit.app/)** | Grounded Q&A over specifications, safety manuals, and method statements, returning source excerpts alongside every answer plus structured document summaries. Ingests PDF, DOCX, TXT, and Markdown. | Python, OpenAI API, PyPDF, python-docx, Pydantic, Streamlit |
| [Inspection Report Generator](https://github.com/R-SAMSAMI/inspection-report-generator) · **[live demo](https://rei-inspection-report.streamlit.app/)** | Field and drone photos to structured defect findings, severity assessment, GPS-aware map context, and report-ready summaries. | Python, OpenAI Responses API, Pillow, Pydantic, geopy |
| [Construction Safety Copilot](https://github.com/R-SAMSAMI/construction-safety-copilot) | Multimodal hazard review and safety reporting from site images and field context. The single-pass predecessor to the agentic version above. | Python, OpenAI API, multimodal AI, Streamlit |
| [Agent Output Watchdog](https://github.com/R-SAMSAMI/agent-output-watchdog) · **[live demo](https://rei-agent-output-watchdog.streamlit.app/)** | Runtime monitoring for an LLM/RAG agent: scores every response for grounding, logs each run to Delta Lake, detects anomalies (z-score) and distribution drift (PSI), and escalates incidents to a human-review queue. | Python, LangChain, Delta Lake, Streamlit, LLM evaluation |

### Machine learning and decision support

| Project | What it demonstrates | Stack |
| --- | --- | --- |
| [BridgeWatch](https://github.com/R-SAMSAMI/bridgewatch) | Inspection-priority triage across the **FHWA National Bridge Inventory** — real federal data, not a toy set. State-level exploration, an interpretable decision tree benchmarked against a random forest, and a per-bridge explanation path showing why an asset was flagged. | scikit-learn, pandas, Streamlit |
| [Project Risk Predictor](https://github.com/R-SAMSAMI/project-risk-predictor) · **[live demo](https://rei-risk-predictor.streamlit.app/)** | Schedule-delay and budget-overrun prediction from 16+ planning fields via 3 Random Forest models (2 classifiers, 1 regressor). Delay-score reliability 0.796, budget-score reliability 0.855, mean delay gap 14.2 days across 3,500 project records, with what-if analysis and visible risk drivers. Synthetic data generated to a realistic planning schema. | scikit-learn, pandas, NumPy, Plotly, Streamlit |
| [Construction Safety SQL](https://github.com/R-SAMSAMI/construction-safety-sql) · **[live demo](https://rei-safety-sql.streamlit.app/)** | 5-table relational safety model (projects, contractors, hazard reports, incidents, corrective actions) with KPI dashboarding, high-risk work zone identification, and corrective-action aging. Synthetic records to a realistic schema. | SQL, SQLite, Python, pandas, Streamlit |
| [Asphalt Plant Risk Tool](https://github.com/R-SAMSAMI/asphalt-ai-tool) | Operational risk estimation and corrective recommendations from plant conditions, using a deliberately interpretable model so operators can see the drivers. | Python, scikit-learn, Streamlit |

### Computer vision, field, and spatial AI

| Project | What it demonstrates | Stack |
| --- | --- | --- |
| [Faithful but Not Plausible? XAI for Bridge Deck Crack Detection](https://github.com/R-SAMSAMI/xai-crack-detection) | Separates whether a saliency map reflects what the model used (faithfulness, via deletion/insertion curves) from whether an inspector can act on it (plausibility, via a blinded expert rating study). Grad-CAM++, Eigen-CAM, Score-CAM, and SHAP across ResNet-18, MobileNetV3-Small, and ViT-Tiny, plus cross-dataset localization against pixel-level crack masks. All four methods score comparably on faithfulness; only three put the highlight on the crack. engrXiv preprint, under review at TRB. | Python, PyTorch, timm, grad-cam, SHAP, XAI evaluation, human-subject rating |
| [Thermal Bridge Detection](https://github.com/R-SAMSAMI/thermal-bridge-detection) | YOLO-based thermal anomaly detection on UAS thermal imagery. | YOLO, PyTorch, thermal imaging |
| [BridgeTwin Inspector](https://github.com/R-SAMSAMI/bridgetwin-inspector) · **[live demo](https://rei-bridgetwin.streamlit.app/)** | 3D plan-versus-scan analysis: generates a structural bridge model, simulates an observed scan with deviation and noise, then classifies every element as on-plan, shifted, missing, or extra. | Python, scikit-learn, 3D visualization |
| [UAV Bridge Inspection Mapping](https://github.com/R-SAMSAMI/spatial-bridge-inspection) | GPS metadata extracted straight from UAS imagery into geolocated inspection points, published both as an interactive Python map and a live ArcGIS Online layer. | Python, geospatial analytics, ArcGIS |
| [Drone Vision-Language Navigation](https://github.com/R-SAMSAMI/drone-vln) | Two-drone cooperative rescue search where the target location is hidden at mission start. Drones search on local nadir camera footprints, natural-language hints act as a search prior rather than coordinates, and response hands off to the best-positioned drone. | Python, vision-language models, multi-agent search |

Data provenance is stated per project. BridgeWatch runs on the public FHWA National Bridge Inventory and the grounding benchmark on public CTDOT, OSHA, and FHWA publications. Where a project uses synthetic records, the row says so — the schemas come from real workflows, the records are generated so the repository can stay public.

---

## How I Build

```text
messy domain data
    -> structured extraction
    -> cleaned analytical layer
    -> interpretable model or AI workflow
    -> measured against something before anyone trusts it
    -> usable product for decision support
```

I like problems where the technical work has to survive contact with real users: inspectors, superintendents, safety managers, engineers, and agency staff. In practice that means:

- clean data pipelines before flashy models
- schema-validated structured outputs before free-text AI responses
- grounding and citations before confident-sounding answers
- explainability before black-box predictions
- an evaluation number before a launch

---

## Stack

**AI / LLM** — RAG architecture, agentic workflows, structured outputs (Pydantic), prompt engineering, LoRA/QLoRA fine-tuning, multimodal AI, LLM evaluation and benchmarking, hallucination testing  
**ML / CV** — PyTorch, scikit-learn, CNNs, Vision Transformers, YOLO, CLIP / zero-shot, XAI (Grad-CAM++, SHAP, Score-CAM, Eigen-CAM)  
**Data** — Python, SQL, Databricks, Delta Lake, PySpark, ETL, PostgreSQL, MongoDB, Power BI, Tableau  
**Cloud / Apps** — Azure AI Services, Azure AI Search, AWS (Certified Cloud Practitioner), Streamlit, Flask  
**Built environment** — BIM/BrIM, Revit, GIS and spatial analytics, UAS inspection, digital twins, photogrammetry

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-336791?style=flat-square&logo=postgresql&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00AEEF?style=flat-square)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)
![Revit](https://img.shields.io/badge/Revit%20%2F%20BIM-186BFF?style=flat-square&logo=autodesk&logoColor=white)

---

## Research

Published work on AI for infrastructure inspection, with a focus on explainability and evaluation. Selected areas: vision transformers for bridge deck inspection, YOLO-based thermal anomaly detection from UAS imagery, RAG and LLM grounding for inspection Q&A, prompt engineering for generative AI in AEC, and BIM/BrIM inspection workflows with photogrammetry and geospatial data.

Full list: [Google Scholar](https://scholar.google.com/citations?user=6AyoxZ0AAAAJ&hl=en&oi=ao)

Some work is under funding, client, or collaboration restriction and is not public.

---

## Fun Fact

I make one of the best baklavas in the world, and yes, precision matters everywhere.

---

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Reihaneh%20Samsami-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rsamsami)
[![Google Scholar](https://img.shields.io/badge/Google%20Scholar-Publications-4285F4?style=for-the-badge&logo=googlescholar&logoColor=white)](https://scholar.google.com/citations?user=6AyoxZ0AAAAJ&hl=en&oi=ao)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:rsamsami@newhaven.edu)
