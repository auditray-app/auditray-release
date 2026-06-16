# Jeux réels anonymisés

Ce dossier contient des **données d'assurance qualité issues de LINAC en conditions réelles de fonctionnement**, intégralement anonymisées avant contribution.

Ces jeux de données constituent le cœur du référentiel national AuditRay : ils reflètent la diversité des équipements, des protocoles et des pratiques des centres français, et servent de base d'entraînement et de validation pour les algorithmes d'IA en physique médicale.

---

## Pourquoi des données réelles ?

Les données synthétiques ne capturent pas toujours les artefacts, les dérives lentes, les comportements atypiques ou les situations limites rencontrées en clinique. Les jeux de données réels permettent de :

- **Valider des algorithmes** dans des conditions proches de la pratique quotidienne
- **Détecter des biais** que les données simulées ne reproduisent pas
- **Construire des benchmarks** inter-centres représentatifs des pratiques françaises
- **Former des modèles d'IA** robustes aux variations d'équipements et de protocoles

---

## Règles d'anonymisation obligatoires

> **Aucune donnée de santé à caractère personnel (DCP / PHI) ne doit être présente.**

Avant toute contribution, vérifiez que les tags DICOM suivants ont été supprimés ou remplacés par des valeurs neutres :

| Tag DICOM | Nom | Action |
|---|---|---|
| `(0010,0010)` | PatientName | Supprimer ou remplacer par `ANONYME` |
| `(0010,0020)` | PatientID | Supprimer ou remplacer par un identifiant fictif |
| `(0010,0030)` | PatientBirthDate | Supprimer |
| `(0010,0040)` | PatientSex | Optionnel — supprimer si non pertinent |
| `(0008,0080)` | InstitutionName | Remplacer par `CENTRE_ANONYME` ou supprimer |
| `(0008,1070)` | OperatorsName | Supprimer |
| `(0008,0090)` | ReferringPhysicianName | Supprimer |

**Outil recommandé :** `pydicom` permet d'automatiser l'anonymisation en Python.

```python
import pydicom

ds = pydicom.dcmread("fichier.dcm")
ds.PatientName = "ANONYME"
ds.PatientID = "ID_FICTIF_001"
ds.PatientBirthDate = ""
ds.InstitutionName = "CENTRE_ANONYME"
for tag in [(0x0008, 0x1070), (0x0008, 0x0090)]:
    if tag in ds:
        del ds[tag]
ds.save_as("fichier_anonymise.dcm")
```

---

## Structure attendue des contributions

```
jeux-reels-anonymises/
├── <type-test>_<equipement>_<date>/
│   ├── fichier1.dcm
│   ├── fichier2.dcm
│   └── metadata.json          # Métadonnées du jeu de données (voir format ci-dessous)
└── README.md
```

### Format `metadata.json`

```json
{
  "id": "picket-fence-varian-truebeam-2025-01",
  "test_type": "picket-fence",
  "ansm_controls": ["UC3"],
  "linac_manufacturer": "Varian",
  "linac_model": "TrueBeam",
  "mlc_type": "HD120",
  "energy": "6MV",
  "acquisition_year": 2025,
  "anonymized": true,
  "phi_removed": true,
  "contributor": "Prénom Nom / CHU Anonyme",
  "notes": "Série de 12 images portales, quelques lames présentant une légère dérive."
}
```

---

## Types de données acceptés

| Type de test | Format | Contrôle ANSM |
|---|---|---|
| Picket Fence | DICOM (RTIMAGE) | UC3 |
| Winston-Lutz | DICOM (RTIMAGE) | UC3 |
| VMAT QA | DICOM (RTIMAGE) | UC4 / UC5 |
| Transmission MLC | DICOM (RTIMAGE) | UC3 |
| Starshot | DICOM / TIFF | UC3 |
| Rendement faisceau | DICOM / CSV / Excel | UC2 |
| Taille de champ | CSV / Excel | UC2 |
| Indice gamma | CSV / Excel | UC4 / UC5 |
| Qualité d'image | DICOM (CT / RTIMAGE) | UC6 |

---

## Comment contribuer

1. Anonymisez vos fichiers (voir règles ci-dessus)
2. Créez un sous-dossier nommé `<type>_<equipement>_<annee>`
3. Ajoutez vos fichiers et un `metadata.json`
4. Ouvrez une pull request — consultez [CONTRIBUTING.md](../../CONTRIBUTING.md)

Pour toute question sur l'anonymisation ou la conformité PHI, consultez [SECURITY.md](../../SECURITY.md).
