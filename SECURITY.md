# Signalement de vulnérabilités de sécurité — AuditRay

Merci de prendre le temps de signaler de manière responsable. La sécurité est une priorité absolue pour AuditRay, notamment en raison de la sensibilité des données manipulées dans un contexte médical et réglementaire.

---

## Comment signaler

Utilisez le [signalement privé de vulnérabilité GitHub](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing/privately-reporting-a-security-vulnerability) sur ce dépôt. Cela permet au mainteneur de prendre connaissance du rapport sans exposer les détails publiquement.

Si le signalement privé n'est pas disponible, ouvrez une issue intitulée `security: description courte` **sans** détails d'exploitation — le mainteneur vous contactera via un canal privé.

Pour tout signalement urgent (données patient exposées, accès non autorisé à la plateforme), contactez directement : [kaptan-data-solutions.app/contact](https://www.kaptan-data-solutions.app/contact)

---

## Informations à inclure

- Description de la vulnérabilité et de son impact potentiel.
- Étapes de reproduction — une description minimale suffit, un PoC complet n'est pas requis.
- Versions affectées, si vous les avez identifiées.
- Si la vulnérabilité concerne des données de santé (PHI/DCP), précisez-le explicitement — cela déclenchera un traitement prioritaire.
- Votre souhait d'être crédité dans le correctif (optionnel).

---

## Périmètre de sécurité spécifique à AuditRay

En raison du contexte médical et réglementaire de la plateforme, les vulnérabilités suivantes sont considérées comme critiques :

| Catégorie | Exemples |
|---|---|
| **Données patient (PHI/DCP)** | Exposition de données DICOM identifiables, fuite de métadonnées patient |
| **Intégrité des données d'AQ** | Altération silencieuse des valeurs de contrôle, falsification de rapports ANSM |
| **Accès non autorisé** | Contournement d'authentification, élévation de privilèges entre établissements |
| **API REST publique** | Injection, SSRF, exposition de données inter-tenants |
| **Plugins communautaires** | Exécution de code arbitraire via un plugin malveillant soumis au marketplace |

---

## Ce que vous pouvez attendre

- Accusé de réception sous quelques jours ouvrés.
- Plan de correction ou de mitigation sous **~30 jours** pour les vulnérabilités confirmées.
- Traitement prioritaire sous **72 heures** pour toute vulnérabilité impliquant des données patient.
- Coordinations avec les dépendances upstream si nécessaire (délai plus long).
- Crédit public après publication du correctif, si vous le souhaitez.

---

## Ce dépôt vs. la plateforme SaaS

Ce dépôt public héberge les releases, templates et plugins communautaires. Il ne contient pas le code source de la plateforme AuditRay. Les vulnérabilités de la plateforme SaaS (application web, API, infrastructure) doivent également être signalées ici — elles seront redirigées vers l'équipe KDS compétente.
