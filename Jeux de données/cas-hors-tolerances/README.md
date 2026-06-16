# Cas hors tolérances

Ce dossier contient des **données d'assurance qualité présentant des dépassements de tolérances cliniquement pertinents** — qu'ils soient issus de mesures réelles anonymisées ou générés synthétiquement de manière contrôlée.

Ces cas constituent la ressource la plus rare et la plus précieuse du référentiel : en clinique, les dépassements graves sont peu fréquents, ce qui les rend difficiles à collecter en nombre suffisant pour entraîner des algorithmes de détection fiables.

---

## Pourquoi ces cas sont-ils critiques ?

Un algorithme entraîné uniquement sur des données dans les tolérances apprendra à reconnaître la normalité, mais échouera à détecter les anomalies — précisément les situations où son rôle est le plus important.

Les cas hors tolérances permettent de :

- **Entraîner des modèles de détection d'anomalies** capables d'identifier des dérives avant qu'elles n'atteignent le patient
- **Définir les seuils d'action** par retours d'expérience multi-centres
- **Valider la sensibilité des algorithmes** face à des situations critiques
- **Simuler des scénarios de panne** pour tester les workflows d'alerte d'AuditRay

---

## Classification des cas

Chaque jeu de données doit être classifié selon la gravité du dépassement observé :

| Niveau | Label | Description | Exemple |
|---|---|---|---|
| 1 | `avertissement` | Dépassement du seuil d'action mais inférieur au seuil d'intervention | Erreur MLC entre 1 et 2 mm |
| 2 | `intervention` | Dépassement du seuil d'intervention — traitement suspendu | Erreur MLC > 2 mm |
| 3 | `critique` | Défaillance majeure identifiée | Feuille MLC bloquée, erreur d'isocentre > 2 mm |

---

## Types de cas recherchés

| Test | Dépassement typique | Contrôle ANSM |
|---|---|---|
| Picket Fence | Erreur de position de lame > seuil d'action | UC3 |
| Winston-Lutz | Écart isocentre > 1 mm | UC3 |
| Starshot | Rayon de l'étoile > tolérance | UC3 |
| Rendement faisceau | Dérive output > 2 % | UC2 |
| Taille de champ | Écart > 2 mm | UC2 |
| VMAT QA / Gamma index | Taux de passage gamma < 95 % (3%/3mm) | UC4 / UC5 |
| Transmission MLC | Transmission résiduelle anormalement élevée | UC3 |
| Qualité d'image | MTF ou CNR hors spécification | UC6 |

---

## Structure attendue des contributions

```
cas-hors-tolerances/
├── <type-test>_<niveau>_<description-courte>/
│   ├── fichiers de données (DICOM, CSV...)
│   ├── rapport_analyse.json     # Résultat de l'analyse et valeurs mesurées
│   └── metadata.json
└── README.md
```

### Format `metadata.json`

```json
{
  "id": "picket-fence-intervention-feuille-bloquee-001",
  "test_type": "picket-fence",
  "ansm_controls": ["UC3"],
  "severity_level": 2,
  "severity_label": "intervention",
  "linac_manufacturer": "Varian",
  "linac_model": "TrueBeam",
  "mlc_type": "HD120",
  "is_real": true,
  "is_synthetic": false,
  "anonymized": true,
  "phi_removed": true,
  "observed_value": 2.4,
  "observed_unit": "mm",
  "action_threshold": 1.0,
  "intervention_threshold": 2.0,
  "outcome": "Traitement suspendu. LINAC remis en service après recalibration MLC.",
  "contributor": "Prénom Nom / Centre anonymisé",
  "notes": "Feuille n°47 présentant une erreur de position progressive sur 3 semaines."
}
```

### Format `rapport_analyse.json`

```json
{
  "analysis_tool": "pylinac.PicketFence",
  "analysis_version": "3.15.0",
  "max_error_mm": 2.4,
  "mean_error_mm": 0.38,
  "failed_leaves": [47],
  "passed": false,
  "tolerance_mm": 1.0,
  "action_level_mm": 2.0
}
```

---

## Règles spécifiques à ce dossier

> [!WARNING]
> Les cas hors tolérances issus de données réelles sont particulièrement sensibles : ils peuvent permettre d'identifier un équipement ou un centre si la situation est suffisamment spécifique. **Redoublez de vigilance lors de l'anonymisation.**

- Supprimez toutes les références à la date exacte de l'incident (n'indiquez que l'année).
- Remplacez le nom du centre par `CENTRE_ANONYME_[A-Z]` (lettre aléatoire).
- Ne mentionnez pas le nom du médecin, du physicien ou du patient impliqué.
- Si le cas a fait l'objet d'un rapport d'incident ANSM, n'incluez pas le numéro de rapport.

---

## Comment contribuer

1. Anonymisez rigoureusement vos données (voir règles ci-dessus + [SECURITY.md](../../SECURITY.md))
2. Classifiez le niveau de gravité (`avertissement`, `intervention`, `critique`)
3. Créez un sous-dossier nommé `<type>_<niveau>_<description>`
4. Ajoutez vos fichiers, `metadata.json` et `rapport_analyse.json`
5. Ouvrez une pull request — consultez [CONTRIBUTING.md](../../CONTRIBUTING.md)

> Ces cas sont particulièrement précieux pour la communauté. Merci de les partager — chaque retour d'expérience contribue à la sécurité des patients en radiothérapie.
