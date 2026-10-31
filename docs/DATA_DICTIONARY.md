# Data dictionary / Veri sözlüğü

> ⚠️ **Fully synthetic data — not real patients. / Tamamen sentetik veridir — gerçek hasta değildir.**
> Not for clinical decision making. / Klinik karar için kullanılamaz.

One row = one adult (≥18 y) emergency department visit. / Her satır = bir erişkin (≥18 yaş) acil servis başvurusu.

| Column | Type | Unit / values | English | Türkçe |
|---|---|---|---|---|
| `visit_id` | string | `SYN-…` | Synthetic visit identifier | Sentetik başvuru kimliği |
| `arrival_datetime` | string (ISO) | 2025-01-01 … 2025-12-31 | Arrival date-time | Başvuru tarihi-saati |
| `age` | int | years, 18–100 | Age | Yaş |
| `sex` | category | `F`, `M` | Sex | Cinsiyet (K=F, E=M) |
| `arrival_mode` | category | `Ambulans`, `Ayaktan` | Arrival by ambulance / walk-in | Geliş şekli |
| `chief_complaint_tr` | category | free-text-like | Chief complaint (Turkish) | Başvuru şikâyeti (Türkçe) |
| `chief_complaint_en` | category | | Chief complaint (English) | Başvuru şikâyeti (İngilizce) |
| `triage_color` | category | `Kırmızı`, `Sarı`, `Yeşil` | Turkish 3-colour triage | Renk kodlu triyaj |
| `esi_level` | int | 1 (most urgent) – 5 | Emergency Severity Index | Acil Ciddiyet İndeksi |
| `sbp_mmhg` | int | mmHg | Systolic blood pressure | Sistolik kan basıncı |
| `dbp_mmhg` | int | mmHg | Diastolic blood pressure | Diyastolik kan basıncı |
| `heart_rate_bpm` | int | beats/min | Heart rate | Nabız |
| `resp_rate_min` | int | breaths/min | Respiratory rate | Solunum sayısı |
| `temperature_c` | float | °C | Body temperature | Vücut ısısı |
| `spo2_pct` | int | % | Peripheral oxygen saturation | Oksijen satürasyonu |
| `on_oxygen` | bool | | Supplemental oxygen at triage | Triyajda oksijen desteği |
| `gcs` | int | 3–15 | Glasgow Coma Scale | Glasgow Koma Skalası |
| `pain_score_0_10` | int | 0–10 | Numeric pain score | Ağrı skoru |
| `htn` | bool | | Hypertension | Hipertansiyon |
| `diabetes` | bool | | Diabetes mellitus | Diyabet |
| `cad` | bool | | Coronary artery disease | Koroner arter hastalığı |
| `copd` | bool | | COPD | KOAH |
| `ckd` | bool | | Chronic kidney disease | Kronik böbrek hastalığı |
| `active_cancer` | bool | | Active malignancy | Aktif malignite |
| `wbc_10e9_l` | float | ×10⁹/L | White blood cells | Lökosit |
| `hgb_g_dl` | float | g/dL | Haemoglobin | Hemoglobin |
| `plt_10e9_l` | int | ×10⁹/L | Platelets | Trombosit |
| `creatinine_mg_dl` | float | mg/dL | Creatinine | Kreatinin |
| `glucose_mg_dl` | int | mg/dL | Glucose | Glukoz |
| `sodium_mmol_l` | int | mmol/L | Sodium | Sodyum |
| `potassium_mmol_l` | float | mmol/L | Potassium | Potasyum |
| `crp_mg_l` | float | mg/L | C-reactive protein | C-reaktif protein |
| `lactate_mmol_l` | float | mmol/L | Lactate | Laktat |
| `hs_troponin_i_ng_l` | int | ng/L | High-sensitivity troponin I | Yüksek duyarlıklı troponin I |
| `icd10_primary` | category | ICD-10 code | Primary ED diagnosis | Birincil acil tanısı (ICD-10) |
| `diagnosis_tr` | category | | Diagnosis label (Turkish) | Tanı adı (Türkçe) |
| `diagnosis_en` | category | | Diagnosis label (English) | Tanı adı (İngilizce) |
| `disposition_tr` | category | Taburcu, Servis yatışı, Yoğun bakım yatışı, Sevk, Kendi isteğiyle ayrıldı, Acilde exitus | Disposition (Turkish) | Sonlanım (Türkçe) |
| `disposition_en` | category | Discharged, Ward admission, ICU admission, Transferred, Left against medical advice, Died in ED | Disposition (English) | Sonlanım (İngilizce) |
| `ed_los_min` | int | minutes | ED length of stay | Acilde kalış süresi |
| `hospital_los_days` | int | days (admitted only) | Hospital length of stay | Hastanede yatış süresi |
| `mortality_30d` | bool | | All-cause death within 30 days | 30 günlük mortalite |
| `news2` | int | 0–20 | NEWS2 computed from recorded vitals | Kayıtlı vitallerden NEWS2 |
| `shock_index` | float | HR/SBP | Shock index | Şok indeksi |
| `qsofa` | int | 0–3 | qSOFA computed from recorded values | qSOFA |

## Missing values / Eksik değerler

- **Laboratory columns** are empty when the test would not plausibly have been ordered (structural missingness). / Laboratuvar sütunları, test istenmeyecek başvurularda boştur (yapısal eksiklik).
- **Vital signs** have ~3–7 % missingness, more frequent for low-acuity and night-time visits (MAR). / Vitallerde düşük aciliyette ve gece daha sık olan ~%3–7 eksiklik (MAR).
- **Cardiac arrest** visits have no arrival vitals (unmeasurable). / Kardiyak arrest başvurularında geliş vitalleri yoktur.
- `news2`, `shock_index`, `qsofa` are empty when a required component is missing. / Bileşeni eksikse türetilmiş skorlar boştur.
- `hospital_los_days` is empty unless admitted (ward/ICU). / Yatış yoksa boştur.
