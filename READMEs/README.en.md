<h1 align="center">
  <img src="../AuditRay_img.png" alt="AuditRay" width="720" />
</h1>

<p align="center">
  <strong>Radiotherapy quality control, finally unified.</strong><br />
  <em>Centralize your 135 ANSM controls, automate your analyses, and generate audit reports in one click.</em>
</p>

<p align="center">
  <a href="../README.md">Français</a> |
  <a href="README.en.md">English</a> |
  <a href="README.es.md">Español</a> |
  <a href="README.de.md">Deutsch</a> |
  <a href="README.it.md">Italiano</a> |
  <a href="README.pt.md">Português</a> |
  <a href="README.ja.md">日本語</a> |
  <a href="README.zh.md">中文</a>
</p>

<p align="center">
  <a href="https://www.kaptan-data-solutions.app/upcoming_saas"><img src="https://img.shields.io/badge/🚀_Early_Access-Join_the_list-E8622A?style=flat-square" alt="Early Access" /></a>
  <a href="https://kaptan-data-solutions.app/"><img src="https://img.shields.io/badge/Official_Site-AuditRay-E8622A?style=flat-square&logo=safari&logoColor=white" alt="Official Site" /></a>
  <a href="https://kaptandatasolutions.github.io/"><img src="https://img.shields.io/badge/Blog_KDS-kaptandatasolutions.github.io-1A2B4A?style=flat-square&logo=github&logoColor=white" alt="Blog KDS" /></a>
  <a href="https://github.com/kaptandatasolutions"><img src="https://img.shields.io/badge/Author-kaptandatasolutions-24292e?style=flat-square&logo=github&logoColor=white" alt="kaptandatasolutions" /></a>
  <a href="https://ansm.sante.fr"><img src="https://img.shields.io/badge/ANSM_2023-Compliant-2C9E4A?style=flat-square" alt="ANSM 2023" /></a>
  <a href="#"><img src="https://img.shields.io/badge/135_Controls-UC1–UC8_•_S1–S3-1D7A8A?style=flat-square" alt="135 controls" /></a>
  <a href="../Jeux%20de%20données/README.md"><img src="https://img.shields.io/badge/Datasets-Open_Data-C9962B?style=flat-square&logo=files&logoColor=white" alt="Datasets" /></a>
  <a href="#"><img src="https://img.shields.io/badge/Python-pylinac-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python pylinac" /></a>
  <a href="#"><img src="https://img.shields.io/badge/Format-DICOM_•_CSV_•_PTW_•_IBA-6366F1?style=flat-square" alt="Formats" /></a>
  <a href="../SECURITY.md"><img src="https://img.shields.io/badge/PHI--Free-Anonymized_Data-E8622A?style=flat-square&logo=shield&logoColor=white" alt="PHI Free" /></a>
</p>

---

<p align="center">
  <a href="https://www.kaptan-data-solutions.app/upcoming_saas">
    <img src="https://img.shields.io/badge/🚀%20Early%20Access%20—%20Join%20the%20pioneer%20physicists%20list-Free%20registration-E8622A?style=for-the-badge" alt="Join the waitlist" />
  </a>
</p>

> **A radiotherapy department produces dozens of quality controls per week, scattered across heterogeneous tools. How do you guarantee traceability, ANSM compliance, and data capitalisation — while saving time?**

**AuditRay** is the SaaS platform that unifies all your LINAC quality controls around a native ANSM 2023 architecture, an open Python analysis hub, and a community ecosystem of scripts and templates.

> *The goal is not a dashboard that impresses — it's a platform that makes your daily QA reliable and frees up time for what matters.*

---

## About this repository

This repository hosts the **public releases of AuditRay**, official documentation, report templates, reference datasets, and community integration guides.

**AuditRay is not open-source** — this repository does not contain the source code of the main platform. It is however open to community contributions via the public API and the template/plugin system.

<p align="center">
  <strong>A project by <a href="https://github.com/kaptandatasolutions">kaptandatasolutions</a></strong><br />
  <em>Find our articles and tutorials on the <a href="https://kaptandatasolutions.github.io/">KDS Blog</a> — medical physics, Python, AI, and radiotherapy QA.</em>
</p>

---

## ✨ Features

> [!NOTE]
> This repository also contains a collection of **anonymized DICOM and Excel datasets** to test your analysis scripts. See the [`Jeux de données/`](../Jeux%20de%20données/README.md) folder.

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>🏗️ Native ANSM 2023 Architecture</h3>
      <p>All 135 controls (UC1–UC8, S1–S3) are modeled directly into the data structure and workflows. No post-hoc document reconstruction.</p>
    </td>
    <td width="50%" valign="top">
      <h3>📥 Multi-source Import</h3>
      <p>DICOM, CSV, proprietary PTW / IBA formats (when unencrypted). Centralized import engine with full traceability back to the raw measurement.</p>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>🐍 Python Analysis Hub — REST API</h3>
      <p>Each physicist deploys their own analysis modules via the public REST API. Results feed directly into AuditRay compliance dashboards.</p>
    </td>
    <td width="50%" valign="top">
      <h3>📊 Multi-centre Benchmark</h3>
      <p>Compare LINACs of the same type across institutions. Adjust action thresholds based on aggregated real-world experience.</p>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>📄 Audit Reports in One Click</h3>
      <p>Automatic generation of traceable regulatory reports, ready to present during ANSM inspections.</p>
    </td>
    <td width="50%" valign="top">
      <h3>🤝 Community Ecosystem</h3>
      <p>Marketplace of analysis plugins and report templates developed by the French and international medical physics community.</p>
    </td>
  </tr>
</table>

---

## 🚀 Contributing

### Analysis Plugins

Submit your Python script via a pull request on `community-plugins.json`:

```json
{
  "id": "my-picket-fence-analysis",
  "name": "Picket Fence — My LINAC",
  "author": "First Last / Hospital Name",
  "description": "UC3 analysis — MLC positioning for Varian TrueBeam.",
  "ansm_controls": ["UC3"],
  "linac_type": ["Varian TrueBeam"],
  "repo": "username/repo-name",
  "language": "Python",
  "requires": ["pylinac>=3.0", "pydicom"]
}
```

> [!IMPORTANT]
> **No patient data (PHI / personal health information) must be included in your contributions.** Always anonymize your DICOM files before committing. See [SECURITY.md](../SECURITY.md) for anonymisation rules.

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the full guide.

---

## 🚀 Early Access — Join the pioneer physicists

> [!IMPORTANT]
> **AuditRay is currently being deployed.** Medical physicists who register now get **priority access**, a **free trial period**, and a **direct voice in the roadmap** — your real-world feedback shapes the platform.

**Why register now?**

- ✅ **Priority access** — be among the first institutions to use AuditRay before the public launch.
- ✅ **Free trial** — test the platform on your own LINAC data with no commitment.
- ✅ **Co-build the product** — your field needs (equipment, protocols, formats) drive the development priorities.
- ✅ **Founding community** — join the pioneer physicists network to share scripts and real-world experience.
- ✅ **ANSM-compliant from day one** — native UC1–UC8 / S1–S3 architecture, no adaptation required.

<p align="center">
  <a href="https://www.kaptan-data-solutions.app/upcoming_saas">
    <img src="https://img.shields.io/badge/👉%20Register%20for%20early%20access-kaptan--data--solutions.app-E8622A?style=for-the-badge" alt="Register" />
  </a>
</p>

<p align="center"><em>Free registration · No commitment · Secure data</em></p>

---

## 🔗 Links

<table>
  <tr>
    <td align="center">
      <a href="https://kaptan-data-solutions.app/">
        <img src="https://img.shields.io/badge/Official_Site-kaptan--data--solutions.app-E8622A?style=for-the-badge&logo=safari&logoColor=white" alt="Official Site" /><br />
        <sub>AuditRay Platform</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://kaptandatasolutions.github.io/">
        <img src="https://img.shields.io/badge/KDS_Blog-kaptandatasolutions.github.io-1A2B4A?style=for-the-badge&logo=github&logoColor=white" alt="Blog KDS" /><br />
        <sub>Articles & Tutorials</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://www.kaptan-data-solutions.app/forum">
        <img src="https://img.shields.io/badge/Community-Physicists_Forum-1D7A8A?style=for-the-badge&logo=discourse&logoColor=white" alt="Forum" /><br />
        <sub>Community Forum</sub>
      </a>
    </td>
    <td align="center">
      <a href="https://www.kaptan-data-solutions.app/contact">
        <img src="https://img.shields.io/badge/Support-Contact_Us-C9962B?style=for-the-badge&logo=mail&logoColor=white" alt="Support" /><br />
        <sub>Support & Contact</sub>
      </a>
    </td>
  </tr>
</table>

---

<p align="center">
  <sub>
    AuditRay is developed and maintained by
    <a href="https://github.com/kaptandatasolutions"><strong>kaptandatasolutions</strong></a>
    —
    <a href="https://kaptan-data-solutions.app/">kaptan-data-solutions.app</a>
    •
    <a href="https://kaptandatasolutions.github.io/">KDS Blog</a>
  </sub><br />
  <sub><em>Thank you for contributing to safer and more efficient radiotherapy quality control.</em></sub>
</p>
