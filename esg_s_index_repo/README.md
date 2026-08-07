# 🏗️ NLP-based S-Index for Russian Real Estate Developers

**HSE University · Faculty of Computer Science · Data Science and Business Analytics · 2025**  
**Authors:** Kirill Budyak, Viktoriia Korableva

A research project that develops a **data-driven Social (S) component of ESG assessment for Russian real estate developers** using customer reviews from CIAN and Avito.

Instead of relying only on corporate disclosures or a simple average star rating, the project analyzes **what customers actually discuss**, **how positive or negative the feedback is**, and **which topics have the strongest impact on trust**.

---

## Business Problem

Traditional ESG assessments are often based on company reports, expert judgement and structured disclosures. For the real-estate market, this can miss an important source of information: the day-to-day experience of customers interacting with developers and residential projects.

The project addresses this gap by converting large volumes of unstructured customer feedback into an interpretable developer-level **S-Index**. The resulting metric can be used as an additional signal for:

- comparing developers from a customer-perception perspective;
- identifying the topics that most strongly influence trust and satisfaction;
- tracking recurring issues such as construction quality or handover delays;
- supporting analytical work for customers, developers and other market stakeholders.

> The project focuses specifically on the **Social / stakeholder-perception dimension** of ESG rather than claiming to replace a full E+S+G rating methodology.

---

## What We Built

The end-to-end research pipeline consists of five stages:

1. **Data collection** — customer reviews were collected from CIAN and Avito for a selected set of major Russian developers.
2. **Data preparation** — reviews and developer metadata were cleaned, normalized and merged into a unified analytical dataset.
3. **Sentiment analysis** — a fine-tuned `ruBERT-large` model classified feedback as negative, neutral or positive.
4. **Topic discovery** — text embeddings, dimensionality reduction, clustering and c-TF-IDF were used to identify interpretable discussion themes.
5. **S-Index calculation** — topic-aware sentiment signals were aggregated into a developer-level trust / social-responsibility score.

### Dataset

- **38** major Russian real estate developers
- **18,048** customer reviews
- Sources: **CIAN** and **Avito**
- Reviews span approximately **2020–2025**

---

## Key Results

### Sentiment model

The final `ai-forever/ruBert-large` classifier was fine-tuned for three-class sentiment analysis.

| Metric | Test result |
|---|---:|
| Accuracy | **0.941** |
| Macro F1 | **0.848** |
| Macro ROC-AUC | **0.955** |

### S-Index validation

Several approaches for topic weighting were compared. The final logistic-regression-based formulation provided the strongest validation results.

| Metric | Final result |
|---|---:|
| Accuracy | **0.895** |
| Macro F1 | **0.879** |
| AUC | **0.944** |
| Spearman correlation with developer rating | **0.897** |

The analysis also showed that different discussion topics affect perceived trust differently: **quality complaints and handover delays reduce trust most strongly**, while positive feedback about family and local infrastructure contributes positively.

---

## S-Index Idea

For every developer, the score combines topic importance with the balance of positive and negative customer feedback in that topic:

\[
S(d) = \sum_k w_k\left(\frac{pos_{d,k}}{N_d} - \frac{neg_{d,k}}{N_d}\right)
\]

where:

- `N_d` — total number of reviews for developer `d`;
- `pos_{d,k}` / `neg_{d,k}` — positive and negative reviews for topic `k`;
- `w_k` — learned importance of the topic.

The score is then rescaled to an intuitive **0–5 range**.

The key idea is that two developers with the same average rating can receive different S-Index values if the underlying reasons for customer dissatisfaction differ. For example, repeated complaints about construction quality or delivery delays should matter more than minor location-related comments.

---

## Kirill Budyak — Project Contribution

My contribution to the joint research project included:

- selection and preparation of the target developer sample;
- deployment and adaptation of the **CIAN data-collection pipeline**;
- development and experimentation with the **ruBERT sentiment-classification pipeline**;
- model evaluation and hyperparameter-search workflow;
- validation of the final **S-Index** and comparison against developer ratings.

The complete division of work and research methodology are documented in the project report under `docs/`.

---

## Repository Structure

```text
.
├── 01_avito_parser.ipynb
├── 02_cian_parser.ipynb
├── 03_merge_scraped_reviews.ipynb
├── 04_sentiment_classification_ruBERT.ipynb
├── 05_topic_modeling_and_s_index.ipynb
├── data/
│   └── README.md
├── docs/
│   └── ESG_in_development_Budyak_Korableva.pdf
├── requirements.txt
├── .gitignore
└── README.md
```

### Notebooks

| Notebook | Purpose |
|---|---|
| `01_avito_parser.ipynb` | Avito review collection workflow used during the research |
| `02_cian_parser.ipynb` | CIAN review / developer-data collection workflow |
| `03_merge_scraped_reviews.ipynb` | Data normalization, developer matching, merging and feature preparation |
| `04_sentiment_classification_ruBERT.ipynb` | ruBERT sentiment classification, Optuna tuning and evaluation |
| `05_topic_modeling_and_s_index.ipynb` | Embeddings, clustering, c-TF-IDF topic analysis and S-Index experiments |

---

## Technology Stack

**Data collection:** Python, browser automation, Playwright / Selenium, BeautifulSoup  
**Data processing:** pandas, NumPy, Natasha  
**NLP / Deep Learning:** PyTorch, Hugging Face Transformers, `ai-forever/ruBert-large`, Sentence Transformers  
**ML / Research:** scikit-learn, Optuna, UMAP, K-Means, HDBSCAN, c-TF-IDF  
**Evaluation & visualization:** SciPy, Matplotlib, Seaborn  
**Workflow:** Jupyter Notebook, Git, GitHub

---

## Running the Research Notebooks

Create and activate a virtual environment, then install the dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
playwright install chromium
```

On Windows:

```powershell
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
playwright install chromium
```

The original research datasets are **not included** in the repository. See `data/README.md` for the expected intermediate file names.

> Web interfaces and anti-bot mechanisms on external platforms change over time. The parser notebooks document the research implementation used for the 2025 project and may require selector updates before being run against current versions of CIAN or Avito.

---

## Research Report

The full project report is included here:

**[`docs/ESG_in_development_Budyak_Korableva.pdf`](docs/ESG_in_development_Budyak_Korableva.pdf)**

It contains the research motivation, literature review, data-collection methodology, model training setup, topic analysis, S-Index formulation, evaluation and conclusions.

---

## Authors

- **Kirill Budyak** — [GitHub](https://github.com/kkkkkkkkkkkirill)
- **Viktoriia Korableva**

Research Team Project, HSE University, Faculty of Computer Science, 2025.
