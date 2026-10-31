---
license: cc-by-nc-4.0
language:
- tr
- en
pretty_name: Turkish ED Synthetic Cohort (5k sample)
size_categories:
- 1K<n<10K
task_categories:
- tabular-classification
- tabular-regression
tags:
- synthetic
- medical
- emergency-medicine
- tabular
- triage
- education
configs:
- config_name: default
  data_files:
  - split: train
    path: data/turkish_ed_synthetic_cohort_sample5k.parquet
---

# Turkish ED Synthetic Cohort · Türkçe Sentetik Acil Servis Kohortu

> [!WARNING]
> **Fully synthetic. Not real patients. Not for clinical decision making.**
> Every row was produced by parametric generation under documented clinical assumptions. No real patient record was used at any stage. Associations in the data are *built in by design*; they are **not** evidence about real-world medicine and must not be published as research findings.
>
> **Tamamen sentetiktir. Gerçek hasta verisi değildir. Klinik karar için kullanılamaz.** Veri, belgelenmiş klinik varsayımlar altında parametrik olarak üretilmiştir; içindeki ilişkiler tasarım gereğidir, gerçek bir bulgu olarak yayımlanamaz.

**5,000 adult emergency department visits × 45 variables** — a seeded random sample of a 50,000-visit synthetic cohort shaped like a Turkish tertiary-care ED record: arrival time, demographics, chief complaint (TR/EN), Turkish colour triage + ESI, vital signs, comorbidities, a realistic lab panel with structural missingness, ICD-10 diagnosis (TR/EN), disposition, ED and hospital length of stay, 30-day mortality, and derived NEWS2 / shock index / qSOFA.

## Why

Real ED data are hard to share. Teaching statistics, data cleaning and clinical ML usually stalls at "we cannot give you the data". This dataset gives students and developers something that **behaves** like an ED registry (skewed labs, digit preference in blood pressure, missing-not-at-random patterns, rare severe outcomes, class imbalance) while carrying **zero privacy risk**.

## Use cases

- **Teaching** biostatistics and epidemiology to medical students and residents (descriptive tables, χ², logistic regression, missing-data handling).
- **Triage model exercises**: predict admission, ICU need or 30-day mortality from triage-time variables; practise calibration, class imbalance and fairness checks.
- **ML / LLM prototyping**: dashboards, data pipelines or bilingual (TR/EN) clinical NLP demos before getting access to real data.
- **Data-cleaning drills**: structural vs random missingness, derived-score recomputation, unit checks.

## Quick start

```python
from datasets import load_dataset
ds = load_dataset("farukdanis/turkish-ed-synthetic-cohort", split="train")
df = ds.to_pandas()
df.groupby("esi_level")["disposition_en"].value_counts(normalize=True)
```

## Files

| Path | Content |
|---|---|
| `data/turkish_ed_synthetic_cohort_sample5k.parquet` / `.csv` | 5,000-row sample |
| `docs/DATA_DICTIONARY.md` | Column definitions, Turkish & English |
| `docs/PARAMETERS.md` | Method statement and cited definitions |
| `docs/VALIDATION.md` | Distribution summaries, sanity checks and figures (computed on the full cohort) |

## Snapshot (full 50k cohort)

| | |
|---|---|
| Median age (IQR) | 45 (33–63) |
| ESI 1 / 2 / 3 / 4 / 5 | 2 % / 14 % / 29 % / 32 % / 23 % |
| Discharged / ward / ICU | 89 % / 9 % / 0.5 % |
| 30-day mortality | 0.8 % |
| Median ED LOS | 164 min |

Rare outcomes (ICU, death in ED) have small counts in the 5k sample. See [`docs/VALIDATION.md`](docs/VALIDATION.md).

## Full cohort, custom cohorts and generator — available on request

- **Full 50,000-visit cohort**
- **Custom cohorts**: any size, case-mix (e.g. cardiology-heavy, geriatric, trauma, sepsis), or scenario (crowding, seasonal surge, mass-casualty-like arrivals)
- **Generator** with documented parametric assumptions, for teaching programmes, hackathons and ML prototyping

Contact: **[faruk.md](https://www.faruk.md)**

## Limitations

- Parametric generation under clinical assumptions; not calibrated to Turkish national data.
- Adults only; no paediatric, obstetric or psychiatric-hold pathways; one diagnosis per visit.
- Labs are single time-point values; no repeat troponins, imaging or treatments.
- Effects are hand-specified — models trained here **will not transfer** to real patients.

## Licence & citation

**CC BY-NC 4.0** — free for non-commercial use with attribution. For commercial use, contact [faruk.md](https://www.faruk.md).

```bibtex
@misc{danis2026turkishedsynthetic,
  author       = {Dan{\i}{\c s}, Faruk},
  title        = {Turkish ED Synthetic Cohort: a fully synthetic, bilingual emergency department dataset for teaching and prototyping},
  year         = {2026},
  howpublished = {\url{https://huggingface.co/datasets/farukdanis/turkish-ed-synthetic-cohort}},
  note         = {ORCID 0000-0001-8722-5402}
}
```

**Author:** Faruk Danış, MD — Emergency Medicine, Bolu Abant İzzet Baysal University · [ORCID 0000-0001-8722-5402](https://orcid.org/0000-0001-8722-5402) · [faruk.md](https://www.faruk.md)
