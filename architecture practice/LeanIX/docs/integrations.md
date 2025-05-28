
# 🔄 How This Is Achieved: Integrating Confluence / SharePoint with LeanIX

Use **Confluence or SharePoint as presentation layers** while **LeanIX remains your architecture system of record**. This setup enables dynamic documents like the Solution Architecture Document (SAD), Target State Architecture (TSA), or Current State Assessment (CSA) with live LeanIX data.

---

<details>
<summary>🧩 1. LeanIX – Confluence Integration (Most Mature)</summary>

### ✅ Key Capabilities

- Embed **Fact Sheets** (applications, capabilities, projects)
- Insert **architecture diagrams** into pages
- Add **dynamic reports** (e.g., application landscapes, lifecycle views)
- Automatically update content based on latest LeanIX data

### 🔧 How to Implement

1. Install the [LeanIX Confluence Plugin](https://marketplace.atlassian.com/apps/1221049/leanix-confluence-plugin)
2. Authenticate with your LeanIX workspace
3. Use `/leanix` macro in Confluence to insert:
   - Single Fact Sheet view
   - Architecture Diagrams
   - Prebuilt reports (Application Landscape, Tech Radar, etc.)

### 📘 Example Use Case

Create a Solution Architecture Document (SAD) with:

- **Current State**: Application Landscape report
- **Future State**: Embedded Target Architecture Diagram
- **Integration Points**: Interface Circle Map
- **Technology Stack**: Technology Radar

</details>

---

<details>
<summary>🧩 2. LeanIX – SharePoint Integration</summary>

LeanIX does not offer an official SharePoint integration, but you can **embed content via workarounds**.

### ⚙️ Options

- Embed **LeanIX public reports via iFrames**
- Export LeanIX reports as **images, PDFs, or Excel**, then embed
- Use **Power Automate / Power BI** to pull LeanIX API data

### 🔌 Advanced Integration

Use **LeanIX REST API + Microsoft Power Platform**:

- Connect via LeanIX API
- Fetch Fact Sheets and reports
- Display using **Power BI dashboards** in SharePoint
- Schedule auto-refreshes for near-real-time data

### 📘 Example Use Case

Create a CSA summary SharePoint page with:

- Exported Application Inventory table
- Embedded Power BI widget for application health
- Excel-based Risk Register from LeanIX data

</details>

---

<details>
<summary>📋 Comparison Summary</summary>

| Feature                        | Confluence (Plugin)               | SharePoint (Manual/API)                |
|-------------------------------|-----------------------------------|----------------------------------------|
| Real-time Fact Sheet Embed    | ✅ Yes                             | ⚙️ Possible via Power BI or iFrame      |
| Dynamic Diagrams              | ✅ Yes                             | ❌ Not natively                         |
| Structured Reports            | ✅ Embedded via macros             | ⚙️ Power BI Embed or file export        |
| Document Automation           | ✅ Excellent                       | ⚙️ Custom via Power Automate            |
| Ideal Use Case                | SAD, TSA, CSA documents           | Static summaries, executive dashboards |

</details>

---

<details>
<summary>✅ Recommended Workflow (Confluence)</summary>

1. Create a Confluence page (e.g., `SAD - Project X`)
2. Embed the following using LeanIX macros:
   - Application Landscape (Current State)
   - Target Architecture Diagram
   - Interface Map
   - Technology Stack
   - Risk Register
3. Automate version control using Confluence page history
4. Export to PDF for point-in-time capture if needed

</details>

---

Would you like a [sample markdown SAD structure](#) or a [Power BI integration guide](#) next?
