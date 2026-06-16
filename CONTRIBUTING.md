# Contribuer à AuditRay

Merci de l'intérêt que vous portez à l'écosystème AuditRay. Ce guide décrit comment contribuer efficacement à ce dépôt public — plugins d'analyse, templates de rapports, documentation et remontées de bugs.

---

## Modes de contribution

| Type | Description |
|---|---|
| **Plugin d'analyse** | Script Python automatisant un ou plusieurs contrôles ANSM, soumis via `community-plugins.json` |
| **Template de rapport** | Mise en page personnalisée de rapport d'audit, soumis via `community-templates.json` |
| **Documentation** | Amélioration ou traduction de la documentation existante |
| **Bug report** | Signalement d'un comportement inattendu dans l'API ou les templates |
| **Demande de fonctionnalité** | Proposition d'évolution de la plateforme ou de l'API |

---

## Prérequis

Avant de contribuer, assurez-vous de disposer de :

- **Python 3.9+** — pour développer et tester vos scripts d'analyse
- **Git** — pour la gestion de version
- **pylinac** (optionnel) — pour les analyses d'images LINAC standardisées (Picket Fence, Winston-Lutz, VMAT QA, Starshot)
- **Un compte GitHub** — pour ouvrir des issues et des pull requests
- **Clé API AuditRay** (optionnel) — pour tester l'intégration de vos plugins via l'API REST publique

---

## Démarrage rapide

### 1. Forker et cloner

```bash
git clone https://github.com/<votre-compte>/auditray-release.git
cd auditray-release
```

### 2. Installer les dépendances Python (pour les plugins)

```bash
pip install pylinac numpy pandas pydicom
```

### 3. Tester votre script en local

Votre script doit accepter en entrée un fichier DICOM ou CSV et retourner un JSON structuré conforme au schéma AuditRay. Consultez les exemples dans le répertoire `examples/` pour le format attendu.

### 4. Soumettre

Ajoutez votre entrée dans `community-plugins.json` ou `community-templates.json`, puis ouvrez une pull request.

---

## Workflow de développement

### Créer une branche

Utilisez un nommage descriptif :

```bash
git checkout -b plugin/picket-fence-iba      # Nouveau plugin
git checkout -b fix/template-rapport-pdf     # Correction
git checkout -b docs/guide-api-rest          # Documentation
```

### Convention de commit

```bash
git commit -m "plugin: add IBA MatriXX Picket Fence analysis"
git commit -m "fix: correct UC3 tolerance threshold in template"
git commit -m "docs: add API REST integration guide"
```

Préfixes acceptés :
- `plugin:` — nouveau plugin d'analyse
- `template:` — nouveau template de rapport
- `fix:` — correction de bug
- `docs:` — documentation
- `chore:` — maintenance (mise à jour de dépendances, formatage)

### Ouvrir une pull request

Incluez dans la description :
- Le ou les contrôles ANSM couverts (ex. : UC3, S1)
- L'équipement ciblé si applicable (ex. : Varian TrueBeam, Elekta Versa HD)
- Un exemple de sortie JSON anonymisé
- Des captures d'écran si pertinent

---

## Format des contributions JSON

### Plugin (`community-plugins.json`)

```json
{
  "id": "picket-fence-iba-matrixx",
  "name": "Picket Fence — IBA MatriXX",
  "author": "Prénom Nom / CHU de Ville",
  "description": "Analyse automatisée Picket Fence (UC3) pour détecteur IBA MatriXX. Retourne l'erreur maximale de lame en mm.",
  "ansm_controls": ["UC3"],
  "linac_type": ["Varian TrueBeam", "Elekta Versa HD"],
  "repo": "utilisateur/depot-github",
  "language": "Python",
  "requires": ["pylinac>=3.0", "pydicom"]
}
```

### Template (`community-templates.json`)

```json
{
  "name": "Rapport UC1-UC8 mensuel — CHU",
  "screenshot": "previews/rapport-chu-blurred.png",
  "regulatory_version": "ANSM 2023",
  "controls_covered": ["UC1", "UC2", "UC3", "UC4", "UC5", "UC6", "UC7", "UC8"],
  "author": "Prénom Nom / CHU de Ville"
}
```

---

## Règles impératives

### Données patient (PHI)

> **Aucune donnée de santé à caractère personnel (DCP / PHI) ne doit figurer dans vos contributions.**

- Anonymisez systématiquement les fichiers DICOM avant tout commit (supprimez les tags `PatientName`, `PatientID`, `PatientBirthDate`, etc.).
- Utilisez des données synthétiques ou des fantômes de test.
- En cas de doute, consultez [notre politique de données](https://www.kaptan-data-solutions.app/Data_Policy).

### Qualité du code

- Écrivez du code lisible, avec des noms de variables explicites.
- Ajoutez un commentaire uniquement quand la logique n'est pas évidente.
- Respectez PEP 8 pour Python.
- Ne laissez pas de `print()` de debug dans le code soumis.

---

## Processus de revue

1. **Vérifications automatiques** — format JSON, absence de PHI détectable
2. **Revue par les mainteneurs KDS** — conformité ANSM, qualité du code
3. **Retours** — adressez les modifications demandées dans votre branche
4. **Validation** — fusion dans `main` après approbation
5. **Publication** — votre contribution apparaît dans le marketplace AuditRay

---

## Obtenir de l'aide

- **Issues GitHub** — pour les bugs et demandes de fonctionnalités
- **Forum communautaire** — [kaptan-data-solutions.app/forum](https://www.kaptan-data-solutions.app/forum)
- **Support** — [kaptan-data-solutions.app/support_ticket](https://www.kaptan-data-solutions.app/support_ticket)

---

## Licence des contributions

En soumettant une contribution, vous acceptez qu'elle soit distribuée sous la licence de ce dépôt et intégrée au marketplace AuditRay. Votre nom ou celui de votre établissement sera crédité dans les métadonnées du plugin ou du template.

---

*Merci de contribuer à la communauté AuditRay et à la sécurité des patients en radiothérapie.*
