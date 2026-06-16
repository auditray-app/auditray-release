# Jeux de données — AuditRay

Ce dossier contient les **jeux de données de référence** utilisés pour tester, valider et développer des analyses d'assurance qualité (AQ) compatibles avec la plateforme AuditRay.

Les données sont anonymisées ou synthétiques. **Aucune donnée de santé à caractère personnel (DCP / PHI) n'est présente.**

---

## Structure

```
Jeux de données/
│
│  ── Référentiel national (4 axes) ──────────────────────────────────────
├── jeux-reels-anonymises/   # Données terrain issues de LINAC réels, anonymisées
├── donnees-synthetiques/    # Données générées par script pour l'entraînement IA
├── cas-hors-tolerances/     # Dépassements cliniquement pertinents (rares et précieux)
├── scripts-analyse/         # Scripts Python communautaires, intégrables dans AuditRay
│
│  ── Données de référence par type de test ──────────────────────────────
├── picket-fence/            # UC3 — Contrôle MLC (lames du collimateur multilames)
├── winston-lutz/            # UC3 — Contrôle de l'isocentre mécanique
├── vmat-qa/                 # UC4/UC5 — Contrôle patient VMAT (Clinac iX)
├── mlc-transmission/        # UC3 — Transmission résiduelle des lames MLC
├── starshot/                # UC3 — Rotation gantry / collimateur (Starshot)
├── beam-output/             # UC2 — Rendement et sorties faisceau (MPC)
├── field-size/              # UC2 — Contrôle de la taille de champ
├── gamma-index/             # UC4/UC5 — Contrôle patient : indice gamma
└── image-qualite/           # UC6 — Qualité d'image (CatPhan 504, MV Imager)
```

Les numéros UC renvoient aux unités de contrôle définies par la **décision ANSM du 28/02/2023** relative au contrôle qualité des installations de radiothérapie externe.

---

## Référentiel national — les 4 axes

Ces quatre dossiers forment le cœur du référentiel collaboratif AuditRay, inspiré du schéma présenté au congrès **SFPM 2026**.

| Dossier | Rôle | Lien |
|---|---|---|
| `jeux-reels-anonymises/` | Données terrain issues de LINAC réels, strictement anonymisées | [→ README](jeux-reels-anonymises/README.md) |
| `donnees-synthetiques/` | Données générées par script pour augmenter les volumes d'entraînement IA | [→ README](donnees-synthetiques/README.md) |
| `cas-hors-tolerances/` | Dépassements cliniquement pertinents et rares — cœur de la détection d'anomalies | [→ README](cas-hors-tolerances/README.md) |
| `scripts-analyse/` | Scripts Python communautaires intégrables dans AuditRay via API REST | [→ README](scripts-analyse/README.md) |

---

## Détail des dossiers

### `picket-fence/` — UC3

Contrôle de la position des lames du collimateur multilames (MLC) par acquisition d'images portales.

| Fichier | Équipement | Type |
|---|---|---|
| `AS1000_Picket Fence_2025-06-19.dcm` | Varian AS1000 | Statique |
| `PICKET_FENCE_COMBO.dcm` | Générique | Combo (statique + arc) |
| `PICKET_FENCE_DISTAL.dcm` | Générique | Distal |
| `T0.2_PicketFenceStatic_HD120.dcm` | Varian HD120 MLC | Statique |
| `T0.2_PicketFenceStatic_HD120 (1).dcm` | Varian HD120 MLC | Statique (doublon) |
| `T0.2_PicketFenceStatic_M120.dcm` | Varian M120 MLC | Statique |
| `T1.1_PicketFenceRA_HD120.dcm` | Varian HD120 MLC | Arc rotatif |
| `T1.1_PicketFenceRA_M120.dcm` | Varian M120 MLC | Arc rotatif |
| `RP.TG142_ELEKTA.Versa_PF_EvnM.dcm` | Elekta Versa HD | Lames paires |
| `RP.TG142_ELEKTA.Versa_PF_EvnM (2).dcm` | Elekta Versa HD | Lames paires (doublon) |
| `RP.TG142_ELEKTA.Versa_PF_OddM.dcm` | Elekta Versa HD | Lames impaires |

**Analyse recommandée :** `pylinac.PicketFence`

---

### `winston-lutz/` — UC3

Contrôle de la coïncidence entre l'isocentre mécanique du LINAC et le centre de rotation du faisceau (test de Winston-Lutz).

| Fichier | Description |
|---|---|
| `winstonlutz1.dcm` à `winstonlutz8.dcm` | Série d'images portales multi-angles (bille BB) |
| `wl_file.zip` | Archive complète de la série Winston-Lutz |

**Analyse recommandée :** `pylinac.WinstonLutz`

---

### `vmat-qa/` — UC4 / UC5

Contrôle patient VMAT (Volumetric Modulated Arc Therapy) sur Clinac iX (Varian, 2017). Images portales acquises lors de la délivrance de plans de traitement de référence.

| Fichier | Plan | Type |
|---|---|---|
| `RI.999_ClinaciX_2017.OpenBmT2-1_1_7 (3)_VMAT2.dcm` | VMAT plan T2 | Image ouverte |
| `RI.999_ClinaciX_2017.T2_DR_GS-0_1_8 (3)_VMAT2.dcm` | VMAT plan T2 | Image de référence |
| `RI.999_ClinaciX_2017.OpenBmT3-1_1_14_vmat3.dcm` | VMAT plan T3 | Image ouverte |
| `RI.999_ClinaciX_2017.T3MLCSpeed-0_1_1 (3)_vmat3.dcm` | VMAT plan T3 | Test vitesse MLC |

**Analyse recommandée :** `pylinac.VMAT`

---

### `mlc-transmission/` — UC3

Contrôle de la transmission résiduelle des lames MLC (lumière parasite à travers les lames fermées) et tests de bandes MLC (strip tests).

| Fichier | Description |
|---|---|
| `mlctrans1.dcm` à `mlctrans10.dcm` | Série de 10 images de transmission MLC |
| `RTIMAGE_MLC_STRIP_TEST_1.dcm` | Test de bande MLC — séquence 1 |
| `RTIMAGE_MLC_STRIP_TEST_2.dcm` | Test de bande MLC — séquence 2 |

**Analyse recommandée :** `pylinac.Dynalog` ou analyse personnalisée via l'API AuditRay.

---

### `starshot/` — UC3

Test de Starshot pour le contrôle de la rotation mécanique du gantry et du collimateur. Une étoile de faisceaux est acquise sur film ou détecteur plan.

| Fichier | Description |
|---|---|
| `Gantry_starshot.tif` | Image TIF d'un Starshot gantry |

**Analyse recommandée :** `pylinac.Starshot`

---

### `beam-output/` — UC2

Contrôle du rendement (output) des faisceaux de traitement. Inclut des données Machine Performance Check (MPC) issues d'un TrueBeam (Varian).

| Fichier | Énergie / Type | Description |
|---|---|---|
| `6FFF.dcm` | 6 MV FFF | Image portale — faisceau 6 MV sans filtre égalisateur |
| `10FFF.dcm` | 10 MV FFF | Image portale — faisceau 10 MV sans filtre égalisateur |
| `BEAM_OUTPUT_MPC_TRUEBEAM.xlsx` | Multi-énergies | Export MPC TrueBeam — suivi longitudinal du rendement |

---

### `field-size/` — UC2

Contrôle de la taille de champ : vérification de la conformité entre le champ lumineux et le champ de rayonnement.

| Fichier | Description |
|---|---|
| `FIELD_SIZE_QA.xlsx` | Tableau de suivi des mesures de taille de champ |

---

### `gamma-index/` — UC4 / UC5

Contrôle patient par calcul de l'indice gamma — comparaison entre la distribution de dose planifiée et la dose mesurée. Données issues de Halcyon et TrueBeam (Varian).

| Fichier | Équipement | Description |
|---|---|---|
| `GAMMA_INDEX_PATIENT_QA.xlsx` | Générique | Suivi gamma index — tous équipements |
| `GAMMA_INDEX_PATIENT_QA_HALCYON.xlsx` | Varian Halcyon | Suivi gamma index — Halcyon |
| `GAMMA_INDEX_PATIENT_QA_TRUEBEAM.xlsx` | Varian TrueBeam | Suivi gamma index — TrueBeam |

---

### `image-qualite/` — UC6

Contrôle de la qualité d'image des systèmes d'imagerie embarqués : fantôme CatPhan 504 (imagerie kV/MV) et calibration d'uniformité de l'imageur MV sur Halcyon.

| Fichier | Équipement | Description |
|---|---|---|
| `CatPhan504_DICOM_Files.zip` | Générique | Série DICOM complète du fantôme CatPhan 504 |
| `MV_IMAGER_CALIB_UNIFORMITY_MPC_HALCYON.xlsx` | Varian Halcyon | Calibration uniformité MV Imager — MPC |

**Analyse recommandée :** `pylinac.CatPhan504`

---

## Correspondance ANSM 2023

| Dossier | UC ANSM | Contrôle |
|---|---|---|
| `beam-output/` | UC2 | Rendement, Output, MPC |
| `field-size/` | UC2 | Taille de champ |
| `picket-fence/` | UC3 | Positionnement MLC |
| `winston-lutz/` | UC3 | Isocentre mécanique |
| `mlc-transmission/` | UC3 | Transmission MLC |
| `starshot/` | UC3 | Rotation gantry / collimateur |
| `vmat-qa/` | UC4 / UC5 | Contrôle patient VMAT |
| `gamma-index/` | UC4 / UC5 | Indice gamma patient |
| `image-qualite/` | UC6 | Qualité d'image kV / MV |

---

## Utilisation avec AuditRay

Ces jeux de données peuvent être importés directement dans AuditRay via :

- **L'interface web** — glisser-déposer dans le module d'import correspondant.
- **L'API REST** — endpoint `POST /api/v1/datasets/import` avec le type de contrôle en paramètre.
- **Un plugin communautaire** — les scripts pylinac du marketplace AuditRay acceptent ces formats nativement.

Pour contribuer de nouveaux jeux de données, consultez [CONTRIBUTING.md](../CONTRIBUTING.md).

---

## Licence et anonymisation

Ces fichiers sont fournis à des fins de test, de développement et de validation algorithmique.

- Les fichiers DICOM ont été **anonymisés** : les tags `PatientName`, `PatientID`, `PatientBirthDate` et `PatientAddress` ont été supprimés ou remplacés par des valeurs neutres.
- Les fichiers Excel ne contiennent **aucune information permettant d'identifier un patient**.
- Toute contribution de nouveaux jeux de données doit respecter les mêmes règles — voir [SECURITY.md](../SECURITY.md).
