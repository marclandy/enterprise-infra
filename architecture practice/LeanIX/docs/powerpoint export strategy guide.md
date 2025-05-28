# 🎯 PowerPoint Export Strategy Guide for Enterprise Architecture Practices

This guide helps Enterprise Architects use Confluence and LeanIX effectively to produce stakeholder-ready PowerPoint presentations while maintaining source-of-truth documentation in live systems.

---

## 📘 1. Strategy Overview

- **Author in Confluence** using EA templates (e.g., SAD, TSA, CSA).
- **Embed LeanIX data** with macros for real-time updates.
- **Export selected views** and decisions to PowerPoint for stakeholder engagement.

---

<details>
<summary><strong>🛠️ 2. Tools & Plugins</strong></summary>

### 📎 Confluence

- **LeanIX for Confluence plugin** — embed real-time architecture data.
- **Scroll Exporter (K15t)** — export Confluence pages to PowerPoint.
- **Smartdraw / Gliffy / Lucidchart** — export diagrams used in decks.

### 📊 LeanIX

- Built-in export to PowerPoint for:
  - Application Portfolios
  - Technology Radar
  - Roadmaps
  - Architecture Decisions

</details>

---

<details>
<summary><strong>📑 3. What to Include in PowerPoint</strong></summary>

| Section | Content Source | Notes |
|--------|----------------|-------|
| Executive Summary | Manually authored | Tailor per audience |
| Architecture Diagrams | Exported from LeanIX or Lucidchart | SVG/PNG for clarity |
| Current vs Target State | Embed from Confluence tables | High-level view only |
| Key Decisions | LeanIX Decision Flow export or manual summary | Summarize rationale |
| Roadmap / Milestones | LeanIX or Excel | Include 3–6 month view |
| Risks & Dependencies | From CSA or Risk Register | Focus on top 3–5 only |

</details>

---

<details>
<summary><strong>🔁 4. PowerPoint Creation Process</strong></summary>

1. Draft full content in Confluence using LeanIX macros.
2. Export selected visuals (LeanIX, Lucidchart, diagrams).
3. Use PPT template to align branding and layout.
4. Populate slides from Confluence with:
   - Copy-paste tables/insights
   - Screenshot/insert diagrams
5. Optionally automate with Scroll Exporter or scripts.

</details>

---

<details>
<summary><strong>🚦 5. Governance Tips</strong></summary>

- Tag Confluence pages with labels like `ea-sad`, `ea-tsa`, `ppt-ready`.
- Use a shared folder for stakeholder decks in SharePoint or Teams.
- Maintain "Presentation Views" in LeanIX as standard exports.

</details>

---

## ✅ 6. Recommendations

- **Primary system of record:** Confluence with LeanIX integration.
- **Presentation artifact:** Lightweight, targeted PowerPoint.
- **Automation level:** Start manual, add Scroll Exporter if volume increases.

---

## 📥 Optional Add-ons

- Create a Slide Master in PowerPoint for rapid consistency.
- Maintain a “deck library” with reusable slide components.

---

**For further support or examples, consult your EA Center of Excellence or platform team.**
