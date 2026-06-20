# Données synthétiques

Ce dossier contient des **données d'assurance qualité générées artificiellement**, reproduisant des comportements réalistes de LINAC sans aucun lien avec un patient ou un établissement réel.

Les données synthétiques sont essentielles pour combler les lacunes des jeux de données réels : elles permettent de simuler des cas rares, de générer des volumes suffisants pour l'entraînement de modèles d'IA, et de tester des scénarios extrêmes en toute sécurité.

---

## Pourquoi des données synthétiques ?

| Besoin | Solution synthétique |
|---|---|
| Cas rares difficiles à collecter en clinique | Simulation paramétrique ciblée |
| Volume insuffisant pour entraîner un modèle ML | Génération en grand nombre |
| Tests de robustesse à des valeurs extrêmes | Contrôle total des paramètres d'entrée |
| Absence de contraintes PHI / anonymisation | Aucune donnée patient impliquée |
| Reproductibilité exacte des expériences | Seed aléatoire fixe et traçable |

---

## Types de données synthétiques acceptés

### Images DICOM simulées

Fichiers DICOM générés par script Python reproduisant les caractéristiques physiques d'une image portale (bruit, résolution, artefacts typiques).

**Outils recommandés :**
- `pylinac` — génération de fantômes synthétiques pour Picket Fence, Winston-Lutz, Starshot
- `pydicom` — création et manipulation de fichiers DICOM from scratch
- `numpy` / `PIL` — génération d'images matricielles avec artefacts contrôlés

### Séries temporelles simulées

Tableaux CSV ou Excel reproduisant le suivi longitudinal de paramètres d'AQ (rendement, taille de champ, indice gamma) avec des dérives, des sauts ou des valeurs hors tolérances injectées de manière contrôlée.

### Données issues de modèles physiques

Simulations Monte-Carlo ou calculs analytiques reproduisant la réponse d'un détecteur à une irradiation donnée.

---

## Structure attendue des contributions

```
donnees-synthetiques/
├── <type-test>_<methode-generation>_<version>/
│   ├── fichiers de données (DICOM, CSV, Excel...)
│   ├── generation_script.py     # Script ayant généré ces données
│   └── metadata.json
└── README.md
```

### Format `metadata.json`

```json
{
  "id": "picket-fence-synthetic-v1",
  "test_type": "picket-fence",
  "ansm_controls": ["UC3"],
  "generation_method": "pylinac phantom",
  "generation_script": "generation_script.py",
  "parameters": {
    "num_leaves": 120,
    "mlc_error_range_mm": [-0.5, 0.5],
    "noise_level": 0.02,
    "random_seed": 42
  },
  "num_samples": 100,
  "intended_use": "Entraînement modèle détection dérive MLC",
  "contributor": "Prénom Nom",
  "notes": "Série de 100 images avec erreurs MLC aléatoires uniformes entre -0.5 et +0.5 mm."
}
```

---

## Bonnes pratiques

- **Fixez le seed aléatoire** (`random_seed`) pour garantir la reproductibilité.
- **Documentez les paramètres** de génération dans `metadata.json` — une donnée synthétique sans documentation de ses paramètres perd toute valeur scientifique.
- **Incluez le script de génération** — cela permet à la communauté de générer des variantes et d'auditer la méthode.
- **Validez la plausibilité physique** — les données synthétiques doivent rester dans des plages réalistes pour être utiles à l'entraînement de modèles destinés à la clinique.
- **Précisez l'usage prévu** (`intended_use`) : entraînement, validation, test de robustesse, démonstration.

---

## Exemple minimal — génération d'un Picket Fence synthétique

```python
import numpy as np
import pydicom
from pydicom.dataset import Dataset, FileDataset
from pydicom.uid import generate_uid

def generate_synthetic_picket_fence(
    num_pickets: int = 10,
    mlc_error_mm: float = 0.0,
    noise_level: float = 0.02,
    seed: int = 42,
    output_path: str = "synthetic_pf.dcm"
):
    rng = np.random.default_rng(seed)
    # ... logique de génération ...
    # Sauvegarder en DICOM
    ds = FileDataset(output_path, {}, is_implicit_VR=False, is_little_endian=True)
    ds.file_meta = Dataset()
    ds.file_meta.MediaStorageSOPClassUID = "1.2.840.10008.5.1.4.1.1.481.1"
    ds.file_meta.MediaStorageSOPInstanceUID = generate_uid()
    # PatientName intentionnellement absent — données synthétiques
    ds.save_as(output_path)

generate_synthetic_picket_fence(mlc_error_mm=0.3, seed=42)
```

---

## Comment contribuer

1. Créez un sous-dossier `<type>_<methode>_<version>`
2. Incluez vos fichiers de données, le script de génération et `metadata.json`
3. Ouvrez une pull request — consultez [CONTRIBUTING.md](../CONTRIBUTING.md)
