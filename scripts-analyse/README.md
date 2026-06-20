# Scripts d'analyse

Ce dossier contient les **scripts Python d'analyse d'assurance qualité** développés et partagés par la communauté des physiciens médicaux — intégrables directement dans AuditRay via l'API REST ou utilisables de manière autonome.

Chaque script couvre un ou plusieurs contrôles ANSM (UC1–UC8, S1–S3) et produit un résultat structuré compatible avec les tableaux de bord AuditRay.

---

## Philosophie

> *Un script développé dans un centre et partagé ici bénéficie à l'ensemble de la communauté. Capitaliser sur l'existant plutôt que réinventer la roue dans chaque établissement.*

La mutualisation des scripts d'analyse est l'un des piliers du référentiel national AuditRay. Elle permet de :

- **Harmoniser les pratiques** d'analyse entre centres
- **Réduire la charge de développement** pour chaque physicien
- **Faciliter la validation** des algorithmes par des pairs
- **Accélérer l'adoption de l'IA** en fournissant des bases solides et auditées

---

## Structure du dossier

```
scripts-analyse/
├── picket-fence/                  # UC3 — Scripts MLC Picket Fence
├── winston-lutz/                  # UC3 — Scripts isocentre Winston-Lutz
├── vmat-qa/                       # UC4/UC5 — Scripts contrôle patient VMAT
├── mlc-transmission/              # UC3 — Scripts transmission MLC
├── starshot/                      # UC3 — Scripts Starshot
├── beam-output/                   # UC2 — Scripts rendement faisceau
├── field-size/                    # UC2 — Scripts taille de champ
├── gamma-index/                   # UC4/UC5 — Scripts indice gamma
├── image-qualite/                 # UC6 — Scripts qualité d'image
└── README.md                      # Ce fichier
```

---

## Format d'un script contribué

Chaque script doit être accompagné de son fichier `plugin.json` (pour l'intégration dans le marketplace AuditRay) et d'un `README.md` propre à ce script.

### Arborescence minimale

```
scripts-analyse/<type-test>/<nom-du-script>/
├── analyse.py           # Script principal
├── requirements.txt     # Dépendances Python
├── plugin.json          # Métadonnées pour le marketplace AuditRay
├── README.md            # Documentation du script
└── examples/
    ├── input/           # Exemple de données d'entrée (anonymisées)
    └── output/          # Exemple de sortie JSON attendue
```

### Format `plugin.json`

```json
{
  "id": "picket-fence-hd120-varian",
  "name": "Picket Fence — Varian HD120 MLC",
  "version": "1.0.0",
  "author": "Prénom Nom",
  "institution": "CHU Anonyme",
  "description": "Analyse automatisée Picket Fence (UC3) pour MLC Varian HD120. Retourne l'erreur maximale et moyenne par lame en mm, avec détection des lames en dépassement.",
  "ansm_controls": ["UC3"],
  "linac_compatibility": ["Varian TrueBeam", "Varian Clinac iX"],
  "input_format": ["DICOM RTIMAGE"],
  "output_format": "JSON",
  "requires": ["pylinac>=3.0", "pydicom>=2.4", "numpy>=1.24"],
  "entry_point": "analyse.py",
  "auditray_compatible": true,
  "license": "MIT"
}
```

### Format de sortie attendu (JSON AuditRay)

Tous les scripts doivent retourner un JSON structuré conforme au schéma AuditRay :

```json
{
  "plugin_id": "picket-fence-hd120-varian",
  "plugin_version": "1.0.0",
  "timestamp": "2025-06-16T14:32:00Z",
  "ansm_controls": ["UC3"],
  "passed": true,
  "results": {
    "max_error_mm": 0.42,
    "mean_error_mm": 0.18,
    "tolerance_mm": 1.0,
    "failed_leaves": [],
    "leaf_errors_mm": {
      "1": 0.12, "2": 0.18, "3": 0.42
    }
  },
  "metadata": {
    "linac": "Varian TrueBeam",
    "energy": "6MV",
    "analysis_tool": "pylinac.PicketFence",
    "analysis_version": "3.15.0"
  }
}
```

---

## Interface avec l'API REST AuditRay

Les scripts de ce dossier peuvent être déployés comme plugins AuditRay via l'API REST publique :

```bash
# Soumettre une analyse via l'API AuditRay
curl -X POST https://api.auditray.io/v1/analyses \
  -H "Authorization: Bearer <VOTRE_CLÉ_API>" \
  -H "Content-Type: multipart/form-data" \
  -F "plugin_id=picket-fence-hd120-varian" \
  -F "file=@mesure_pf.dcm"
```

Le résultat JSON est automatiquement intégré dans votre tableau de bord AuditRay et lié au contrôle UC correspondant.

---

## Bonnes pratiques de développement

- **Utilisez `pylinac`** comme base — les algorithmes sont validés et maintenus activement.
- **Gérez les exceptions** proprement : un script qui plante silencieusement est dangereux en contexte clinique.
- **Loguez les avertissements** : si une image est de mauvaise qualité, signalez-le dans le JSON de sortie plutôt que de calculer un résultat potentiellement faux.
- **Testez sur les jeux de données** du dossier [`../jeux-reels-anonymises/`](../jeux-reels-anonymises/) et [`../cas-hors-tolerances/`](../cas-hors-tolerances/).
- **Précisez la compatibilité LINAC** — un script calibré pour un TrueBeam peut ne pas fonctionner sur un Elekta sans adaptation.
- **Versionnez votre script** (`plugin.json` → `version`) pour permettre la traçabilité des analyses dans AuditRay.

---

## Scripts disponibles

> Ce dossier est en construction. Contribuez votre premier script !

| Script | Contrôle ANSM | Équipement | Auteur | Statut |
|---|---|---|---|---|
| *(à venir)* | — | — | — | — |

---

## Comment contribuer

1. Créez un sous-dossier dans la catégorie correspondante : `scripts-analyse/<type-test>/<nom-du-script>/`
2. Ajoutez `analyse.py`, `requirements.txt`, `plugin.json` et `README.md`
3. Incluez des exemples d'entrée/sortie dans `examples/`
4. Testez votre script sur au minimum un jeu de données du référentiel
5. Ouvrez une pull request — consultez [CONTRIBUTING.md](../CONTRIBUTING.md)

Pour soumettre votre script au marketplace AuditRay, ajoutez également votre entrée dans [`community-plugins.json`](../community-plugins.json) à la racine du dépôt.
