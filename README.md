## About this repo

This repo is used for hosting public releases of **AuditRay**, as well as our official documentation, templates, and integration guides.

**AuditRay** is not open-source software and this repo **DOES NOT** contain the source code of the core application. However, if you wish to contribute to the AuditRay ecosystem (custom test templates, automated scripts, or localization), you can do so via our public API and template system.

> **Radiotherapy quality control, finally unified.**
> AuditRay centralizes your 135 controls (ANSM French regulations), automates your analyses, and generates audit reports in one click.
> *Proudly built by KDS.*

---

## Support & Issues

* **Bug Reports & Feature Requests:** This repo does not accept issues related to the core SaaS platform. For support or bug reports, please visit our help center: [https://support.auditray.io]([https://www.google.com/search?q=https://support.auditray.io](https://www.kaptan-data-solutions.app/contact))
* **Community & Feedback:** Join our professional network of medical physicists to discuss ANSM regulations and best practices: [https://community.auditray.io](https://www.kaptan-data-solutions.app/forum)

---

## Contributing to AuditRay

### Submit a Control Template or Plugin

We welcome contributions that help the medical physics community streamline their workflows. Whether it's a specific script for a Linac or an automated analysis for a specific phantom, you can submit your contribution here.

When opening a pull request, please ensure you follow our **submission checklist**. Use the JSON format provided in the directory and we will review your entry.

**Documentation links:**

* [Developer Documentation](https://www.kaptan-data-solutions.app/support_ticket)
* [ANSM Compliance Guide](https://ansm.sante.fr/actualites/decision-du-28-02-2023-fixant-les-modalites-du-controle-de-qualite-des-installations-de-radiotherapie-externe-et-de-radiochirurgie)

---

### Custom Analysis Plugins

To add your automated analysis script to the AuditRay marketplace, make a pull request to the `community-plugins.json` file.

* **id:** A unique ID for your plugin/script.
* **name:** The display name of your analysis.
* **author:** Your name or clinic name.
* **description:** A short description of the 135 ANSM controls covered by this script.
* **repo:** Your GitHub repository identifier (`user-name/repo-name`).

---

### Audit Report Templates

To share a custom report layout, submit your template to the `community-templates.json` file.

* **name:** A unique name for your report style.
* **screenshot:** A blurred or sample path to the report preview.
* **regulatory_version:** The specific ANSM regulation version this report complies with.

---

## Policies

All submissions must comply with our [Developer & Security Policies](https://www.kaptan-data-solutions.app/Data_Policy). Ensure no Patient Health Information (PHI) is included in any test data or screenshots.

## Announcing your Contribution

Once your template or plugin is approved:

1. Share it in our **AuditRay Showcase** forum.
2. Post an update in our **Medical Physicist Discord** in the `#integrations` channel.

*Thank you for helping us make Radiotherapy Quality Control safer and faster!*
