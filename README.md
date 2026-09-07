# Reihaneh (Rei) Samsami

**I build AI systems for work where a wrong answer has consequences, and the evaluation, grounding, and monitoring that prove they hold up.**

Retrieval that actually grounds. Outputs that validate against a schema before a human ever sees them. Explanations someone can audit. Drift caught in production instead of in a postmortem. That is the layer I work on.

My proving ground is construction and infrastructure, because the data is genuinely hostile (site photos, scanned specification books, regulatory standards, CAD and BIM exports) and the person receiving the output is personally accountable for it. **The engineering is not domain-specific.** A benchmark showing that closed-book LLMs are factually unacceptable 56–64% of the time against a regulatory corpus reads the same whether that corpus is a transportation specification, a clinical protocol, or a financial control.

Ph.D. Civil Engineering · M.S. Data Science · Licensed Professional Engineer · AWS Certified Cloud Practitioner
Co-PI, NCHRP 10-110A (Transportation Research Board, 2025–present) · Assistant Professor, University of New Haven

**Open to AI/ML engineering, applied science, and AI governance roles.**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Reihaneh%20Samsami-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rsamsami)
[![Google Scholar](https://img.shields.io/badge/Google%20Scholar-Publications-4285F4?style=for-the-badge&logo=googlescholar&logoColor=white)](https://scholar.google.com/citations?user=6AyoxZ0AAAAJ&hl=en&oi=ao)
[![Email](https://img.shields.io/badge/Email-rsamsami%40newhaven.edu-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:rsamsami@newhaven.edu)

---

## Start Here

You do not need any domain background to read these. Pick the one that matches what you care about.

| If you work on | Read this | Why |
| --- | --- | --- |
| **LLM evaluation, RAG** | [`inspection-llm-grounding`](https://github.com/R-SAMSAMI/inspection-llm-grounding) | 600 scored responses, closed-book vs. RAG vs. full-context, with statistical validation against human experts |
| **AI governance, risk, compliance** | [`construction-ai-risk-assessment`](https://github.com/R-SAMSAMI/construction-ai-risk-assessment) | 288 measured trials, per-function EU AI Act classification, Monte Carlo contingency |
| **Agentic products, structured outputs** | [`agentic-construction-safety-copilot`](https://github.com/R-SAMSAMI/agentic-construction-safety-copilot) | Multimodal agent workflow, schema-enforced end to end, deterministic and live modes |
| **LLMOps, monitoring, drift** | [`agent-output-watchdog`](https://github.com/R-SAMSAMI/agent-output-watchdog) | Per-response grounding scores, Delta Lake run logs, PSI drift, human-review escalation |
| **Explainability, model trust** | [`xai-crack-detection`](https://github.com/R-SAMSAMI/xai-crack-detection) | Faithfulness and plausibility measured separately, with a blinded expert rating study |
| **Data platforms, ETL** | [`bimops-ai`](https://github.com/R-SAMSAMI/bimops-ai) | Medallion lakehouse over messy CAD exports, with a data quality score and a NL query layer |

Seven projects have live demos you can click without installing anything. They are linked inline below.

---

## Featured Work

### Does Grounding Matter? A Controlled LLM Benchmark
**[`inspection-llm-grounding`](https://github.com/R-SAMSAMI/inspection-llm-grounding)** · Submitted to TRB 2027

The question every team shipping an LLM feature against a regulatory document set should have answered first: does grounding actually change whether the answers are defensible, and how much context is it worth paying for?

**Design:** 3 frontier models × 70 validated domain questions × 3 grounding conditions (closed-book, RAG, full-document) = **600 scored responses**, roughly 630 API calls, fully reproducible in Colab. Scoring by an LLM judge held outside the compared set, then validated against human experts.

| Finding | Result |
| --- | --- |
| Ungrounded answers rated factually unacceptable | **56–64%** across all three models |
| Composite score lift from grounding | **+1.3 to +1.7 points** per model (p < 0.000001) |
| Full-document context vs. RAG | **+0.14 average, at ~35× the input tokens** |
| Expert validation of the automated scoring | **Spearman 0.77**, 82.7% within one point (n = 75) |
| Where grounding helps most | Project-specific documents (r = −0.83 with model prior knowledge) |

**Takeaway that generalizes:** closed-book LLMs are not usable for authoritative-source questions. RAG is the right default at corpus scale. The full-context premium is not worth 35× the token spend except on documents the model has never seen.

**Corpus:** public CTDOT, OSHA, and FHWA publications. Code MIT, data and results CC BY 4.0. With Khaled Sayed.
`Python · RAG · LLM-as-judge evaluation · Claude / GPT / Gemini APIs · statistical validation`

---

### Measuring AI Risk on a Real Capital Program
**[`construction-ai-risk-assessment`](https://github.com/R-SAMSAMI/construction-ai-risk-assessment)** · Two engrXiv preprints, Aug 2026

Most AI governance output is a policy document with no numbers under it. This is the measurement layer: what a multi-agent AI platform actually fails at, where the law binds, and how much contingency the residual risk is worth.

- **72-item test set with ground truth**, run through a reproducible evaluation harness, producing **288 raw trial records** with measured failure rates per function
- **Per-function EU AI Act classification** under Regulation (EU) 2024/1689 as amended by the 2026 Digital Omnibus, so each capability gets its own obligation tier rather than one blanket label
- **Monte Carlo contingency simulation** sizing the financial exposure on a $180M program
- Machine-readable risk register, full regulatory corpus, scoring scripts, raw trials, and figure code all in the repo

DOIs: [10.31224/8076](https://doi.org/10.31224/8076) · [10.31224/8077](https://doi.org/10.31224/8077) · CC BY 4.0
`Python · LLM evaluation · EU AI Act · Monte Carlo simulation · risk quantification`

---

### Agentic Safety Review Copilot
**[`agentic-construction-safety-copilot`](https://github.com/R-SAMSAMI/agentic-construction-safety-copilot)** · [![Live demo](https://img.shields.io/badge/Live%20demo-open-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://rei-safety-copilot.streamlit.app/)

A multimodal agent that turns free-text field observations and photographs into structured risk signals, control-gap findings, corrective actions, and a briefing document. Built as a workflow product with a review step, not a prompt wrapper.

- **Pydantic-enforced structured outputs end to end**, so every field is schema-validated before it reaches the person who signs off on it
- **Dual execution modes**: a deterministic offline mode for reproducible demos and regression testing, and a live multimodal mode against the OpenAI Responses API
- Scenario library across 5 distinct work types, with explicit uncertainty handling and human-in-the-loop positioning: the tool drafts, the qualified person decides

Concept direction inspired by [Sharmin Jahan Badhan](https://github.com/sharmin3036); productization and implementation mine.
`Python · OpenAI Responses API · Pydantic · multimodal AI · Streamlit`

---

### Runtime Monitoring for an LLM Agent
**[`agent-output-watchdog`](https://github.com/R-SAMSAMI/agent-output-watchdog)** · [![Live demo](https://img.shields.io/badge/Live%20demo-open-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://rei-agent-output-watchdog.streamlit.app/)

The part that usually does not get built: what happens after the agent is in production. Scores every response for grounding, writes each run to Delta Lake, flags outliers by z-score, detects distribution drift by PSI, and escalates incidents into a human-review queue.

Governance by instrumentation rather than by policy memo. The pattern is portable to any LLM system that needs an audit trail.

`Python · LangChain · Delta Lake · drift detection (PSI) · anomaly detection · Streamlit`

---

### Faithful but Not Plausible? Evaluating XAI Methods
**[`xai-crack-detection`](https://github.com/R-SAMSAMI/xai-crack-detection)** · engrXiv preprint, under review at TRB

A saliency map can be faithful (it reflects what the model actually used) and still be useless (a human cannot act on it). Most XAI papers conflate the two. This one separates them and measures both.

- **Faithfulness** via deletion and insertion curves; **plausibility** via a blinded expert rating study
- Grad-CAM++, Eigen-CAM, Score-CAM, and SHAP compared across **ResNet-18, MobileNetV3-Small, and ViT-Tiny**
- Cross-dataset localization checked against pixel-level ground-truth masks
- **Result:** all four methods score comparably on faithfulness; only three put the highlight on the actual defect. Faithfulness alone does not earn a human's trust.

`Python · PyTorch · timm · grad-cam · SHAP · XAI evaluation · human-subject study`

---

## All Projects

### LLM systems, RAG, and agents

| Project | What it demonstrates | Stack |
| --- | --- | --- |
| [Construction Docs Copilot](https://github.com/R-SAMSAMI/construction-docs-copilot) · **[live demo](https://rei-docs-copilot.streamlit.app/)** | Grounded document Q&A that returns source excerpts alongside every answer, plus structured summarization. Multi-format ingestion: PDF, DOCX, TXT, Markdown. The generic pattern for any authoritative-document assistant. | Python, OpenAI API, PyPDF, python-docx, Pydantic, Streamlit |
| [Inspection Report Generator](https://github.com/R-SAMSAMI/inspection-report-generator) · **[live demo](https://rei-inspection-report.streamlit.app/)** | Vision-language pipeline from raw photographs to structured findings, severity scoring, geospatial context, and a report-ready document. Image in, validated schema out. | Python, OpenAI Responses API, Pillow, Pydantic, geopy |
| [Safety Copilot (v1)](https://github.com/R-SAMSAMI/construction-safety-copilot) | The single-pass predecessor to the agentic version above. Kept public because the two together show the progression from one-shot prompting to a staged agent workflow. | Python, OpenAI API, multimodal AI, Streamlit |

### Machine learning and decision support

| Project | What it demonstrates | Stack |
| --- | --- | --- |
| [BridgeWatch](https://github.com/R-SAMSAMI/bridgewatch) | Priority triage over the **FHWA National Bridge Inventory** — real federal open data, not a toy set. An interpretable decision tree benchmarked against a random forest, plus a per-record explanation path showing why an asset was flagged. Interpretability chosen deliberately, because the output has to be defended. | scikit-learn, pandas, Streamlit |
| [Project Risk Predictor](https://github.com/R-SAMSAMI/project-risk-predictor) · **[live demo](https://rei-risk-predictor.streamlit.app/)** | Schedule-delay and cost-overrun prediction from 16+ planning fields via 3 Random Forest models (2 classifiers, 1 regressor), with what-if analysis and visible risk drivers. Delay-score reliability 0.796, budget-score reliability 0.855, mean delay gap 14.2 days across 3,500 records. Synthetic data to a realistic schema. | scikit-learn, pandas, NumPy, Plotly, Streamlit |
| [Safety Analytics SQL](https://github.com/R-SAMSAMI/construction-safety-sql) · **[live demo](https://rei-safety-sql.streamlit.app/)** | 5-table relational model with KPI dashboarding, high-risk segment identification, and corrective-action aging. Straight relational modelling and analytics engineering, no ML. Synthetic records to a realistic schema. | SQL, SQLite, Python, pandas, Streamlit |
| [Asphalt Plant Risk Tool](https://github.com/R-SAMSAMI/asphalt-ai-tool) | A transparent weighted scoring model over operating conditions that returns a risk estimate plus corrective recommendations. Deliberately rule-based so operators can see every driver and its weight. | Python, Streamlit |

### Computer vision and spatial ML

| Project | What it demonstrates | Stack |
| --- | --- | --- |
| [Thermal Anomaly Detection](https://github.com/R-SAMSAMI/thermal-bridge-detection) | YOLO object detection on drone-captured thermal imagery, locating subsurface anomalies invisible in the visible spectrum. | YOLO, PyTorch, thermal imaging |
| [BridgeTwin Inspector](https://github.com/R-SAMSAMI/bridgetwin-inspector) · **[live demo](https://rei-bridgetwin.streamlit.app/)** | 3D plan-versus-as-built reconciliation: generates a design model, simulates an observed scan with deviation and noise, then classifies every element as on-plan, shifted, missing, or extra. A general digital-twin verification pattern. | Python, scikit-learn, 3D visualization |
| [UAS Inspection Mapping](https://github.com/R-SAMSAMI/spatial-bridge-inspection) | GPS metadata extracted directly from drone imagery into geolocated inspection points, published both as an interactive Python map and a live ArcGIS Online layer. | Python, geospatial analytics, ArcGIS |
| [Drone Vision-Language Navigation](https://github.com/R-SAMSAMI/drone-vln) | Two-agent cooperative search where the target location is hidden at mission start. Agents observe only their local nadir camera footprint, natural-language hints act as a **search prior rather than coordinates**, and the task hands off to the better-positioned agent. Multi-agent VLN under partial observability. | Python, vision-language models, multi-agent search |

### Data engineering and platforms

| Project | What it demonstrates | Stack |
| --- | --- | --- |
| [BIMOps AI](https://github.com/R-SAMSAMI/bimops-ai) | End-to-end medallion architecture turning 17 raw CAD schedule exports across 4 engineering disciplines (~**5,500 records**) into governed Bronze → Silver → Gold tables. Includes a **data-readiness score** that turns metadata completeness into a number a team can act on instead of an opinion, a governance framework with RBAC-aware access design, data dictionaries, and a natural-language query layer over the Gold tables. | Databricks, Delta Lake, PySpark, SQL, Python, Power BI |

### Reference

| Project | What it is |
| --- | --- |
| [AWS Cloud Practitioner Cheatsheet](https://github.com/R-SAMSAMI/aws-cloud-practitioner-cheatsheet) | Study notes from the AWS certification, kept public because people keep asking for them. |

**On data provenance:** every project states its source. BridgeWatch runs on the public FHWA National Bridge Inventory and the grounding benchmark on public CTDOT, OSHA, and FHWA publications. Where a project uses synthetic records the row says so explicitly — the schemas come from real workflows, the rows are generated so the repository can stay public.

---

## How I Build

```text
messy real-world data
 -> structured extraction
 -> a clean analytical layer
 -> an interpretable model or an AI workflow
 -> measured against something before anyone trusts it
 -> monitored after it ships
 -> a decision someone can defend
```

I work on problems where the output reaches a person who is accountable for it. In practice that means:

- clean data pipelines before flashy models
- schema-validated structured outputs before free-text AI responses
- grounding and citations before confident-sounding answers
- explainability that a domain expert can act on, not just a heatmap that scores well
- an evaluation number before a launch, and a drift number after it

---

## Stack

**AI / LLM** — RAG architecture, agentic workflows, structured outputs (Pydantic), prompt engineering, LoRA/QLoRA fine-tuning, multimodal AI, LLM-as-judge evaluation, benchmarking, hallucination testing
**ML / CV** — PyTorch, scikit-learn, CNNs, Vision Transformers, YOLO, CLIP / zero-shot, XAI (Grad-CAM++, SHAP, Score-CAM, Eigen-CAM)
**Data** — Python, SQL, Databricks, Delta Lake, PySpark, ETL, PostgreSQL, MongoDB, Power BI, Tableau
**Cloud / Apps** — Azure AI Services, Azure AI Search, AWS (Certified Cloud Practitioner), Streamlit, Flask
**Governance** — EU AI Act classification, risk registers, evaluation harnesses, drift monitoring (PSI), incident escalation, model documentation
**Domain** — BIM/BrIM, Revit, GIS and spatial analytics, UAS/drone data, digital twins, photogrammetry

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-336791?style=flat-square&logo=postgresql&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00AEEF?style=flat-square)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)

---

## Research

Peer-reviewed and preprint work on applied AI, with a consistent focus on evaluation and explainability rather than benchmark chasing. Selected areas: LLM grounding and RAG evaluation, explainable AI for visual defect detection, vision transformers and YOLO for automated inspection, AI regulatory classification and risk quantification, prompt engineering for applied generative AI, and geospatial and digital-twin data workflows.

Full list: [Google Scholar](https://scholar.google.com/citations?user=6AyoxZ0AAAAJ&hl=en&oi=ao)

Some work is under funding, client, or collaboration restriction and is not public.

---

## Fun Fact

I make one of the best baklavas in the world. Precision matters everywhere.

---

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Reihaneh%20Samsami-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rsamsami)
[![Google Scholar](https://img.shields.io/badge/Google%20Scholar-Publications-4285F4?style=for-the-badge&logo=googlescholar&logoColor=white)](https://scholar.google.com/citations?user=6AyoxZ0AAAAJ&hl=en&oi=ao)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:rsamsami@newhaven.edu)
