# Generation method, sources and assumptions

**Honesty statement.** No real patient record, hospital extract or registry was used. The data were produced by
parametric generation under documented clinical assumptions (a latent-severity model linking vital signs, triage,
laboratory values, disposition and outcome). The numeric parametric assumptions are documented in the full version
of the generator and are not part of this public release. They are clinical assumptions, **not** estimates calibrated
to Türkiye or to any specific hospital.

## Cited definitions (verifiable)

| Element | Source |
|---|---|
| Turkish colour-coded ED triage (kırmızı / sarı / yeşil) — regulatory framework | *Yataklı Sağlık Tesislerinde Acil Servis Hizmetlerinin Uygulama Usul ve Esasları Hakkında Tebliğ*, Resmî Gazete 16.10.2009, No. 27378 (later amended/replaced; e.g. amendment RG 20.02.2018, No. 30338). The ESI→colour mapping in this dataset is a modelling assumption, not taken from the Tebliğ. |
| Emergency Severity Index (ESI) levels 1–5 | Gilboy N, Tanabe P, Travers D, Rosenau AM. *Emergency Severity Index (ESI): A Triage Tool for Emergency Department Care, Version 4. Implementation Handbook.* AHRQ Publication No. 12-0014, 2011 (2012 ed.). |
| NEWS2 scoring (SpO₂ scale 1) | Royal College of Physicians. *National Early Warning Score (NEWS) 2: Standardising the assessment of acute-illness severity in the NHS.* London: RCP; 2017. Consciousness approximated as GCS < 15 → 3 points. |
| qSOFA (RR ≥ 22, SBP ≤ 100, altered mentation) | Seymour CW, et al. *JAMA* 2016;315(8):762–774; Singer M, et al. *JAMA* 2016;315(8):801–810. Altered mentation approximated as GCS < 15. |
| Shock index (HR/SBP) | Allgöwer M, Burri C. *Dtsch Med Wochenschr* 1967;92(43):1947–1950. |
| Diagnosis codes | WHO. *ICD-10: International Statistical Classification of Diseases and Related Health Problems, 10th Revision.* |
