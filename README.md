# AI Agent Security Assessment

A web app for assessing AI agents against ISACA's *Cybersecurity Recommendations for Securing AI Agents* (2026). It covers all 80 controls in the paper's 11 practice categories, rolls them up into ISACA's 15-item Secure by Default checklist, and records data handling decisions based on the paper's Appendix A.

- **Companion workbook:** `AI_Agent_Security_Assessment_Worksheet.xlsx`, the same controls and scoring in Excel. The two exchange data through CSV (see [Import and export](#import-and-export)).

---

## Contents

1. [What it does](#what-it-does)
2. [Quick start](#quick-start)
3. [The tabs](#the-tabs)
4. [Scoring and priorities](#scoring-and-priorities)
5. [Notes](#notes)
6. [Saving and storage](#saving-and-storage)
7. [Sharing and access](#sharing-and-access)
8. [Import and export](#import-and-export)
9. [File formats](#file-formats)
10. [Limits](#limits)
11. [Source material and what was added](#source-material-and-what-was-added)
12. [Troubleshooting](#troubleshooting)
13. [Version history](#version-history)

---

## What it does

- **Assessments:** each assessment covers one AI agent, or one group of agents that share a runtime and toolset. The picker at the top switches between them.
- **Controls:** each of the 80 controls gets a status, a 0–5 maturity rating, evidence, an owner, gap observations, a remediation action, a target date, notes, and an optional criticality override.
- **Calculated results:** coverage by category, average maturity, P1/P2/P3 gap priorities and Secure by Default checklist results, all updated as you work.
- **Notes:** at three levels, per control, per category and for the whole assessment.
- **Import and export:** CSV for spreadsheets and the Excel workbook; JSON for full backup and restore.
- **Saving:** assessments save automatically to the page's own storage, so they persist across sessions and devices.

## Quick start

1. **Open the app in claude.ai** (or the Claude app) while signed in. The status beside the buttons should read **Saved to this page** with a green dot.
2. **Create an assessment.** Click **New assessment**, then fill in the agent name, organization and assessor on **Scope & method**.
3. **Assess the controls.** On **Controls**, click a status and a maturity level for each control. Use the arrow on the right to open the details: evidence, owner, gap, remediation, target date, criticality and notes.
4. **Review the results.** **Overview** shows coverage by category and your open P1/P2 gaps. **Secure by Default** shows the 15 checklist items.
5. **Record the data decisions.** On **Data handling**, set what each data class may do inside the agent.
6. **Export the results.** **Export CSV** gives you a spreadsheet; **Export JSON** gives you a full backup.

The app opens with an assessment labelled **Example: Support triage agent**. It contains sample data to show how the tool works. Delete it once you have a real assessment.

## The tabs

| Tab | What it's for |
|---|---|
| **Overview** | Coverage and average maturity per category as stacked bars (implemented / partial / not / N/A / not assessed). Status totals for all 80 controls. The top open P1 and P2 gaps, with owner and due date. Excerpts of category notes. Click a category name to jump to its controls. |
| **Controls** | All 80 controls grouped by category. Search (ID, control text, evidence, owner, gap, remediation, notes and framework references) and filter by category, status or gap priority. Each category header shows its progress and has an **Add category note** link. |
| **Secure by Default** | ISACA's 15 checklist items. Each one's status is calculated from the controls linked to it; click a control ID to jump to it. An assessor override is available and asks for a written reason. |
| **Data handling** | ISACA's four data classes (Public, Internal, Confidential, Restricted / Highly sensitive). For each, set whether the agent may access it, put it in prompts, keep it in memory, write it to logs, or send it to an external model provider. Also records which agents touch the class, the current state, and the gap. This is the evidence for control DAT-03. |
| **Notes** | A dated log of notes for the assessment, plus a list of all category notes. |
| **Scope & method** | The assessment's details, and the scoring rules written out in full. |

The bar under the header shows coverage, controls assessed, open P1, open P2 and checklist items met, on every tab.

You can link directly to a tab by adding `#overview`, `#controls`, `#checklist`, `#data`, `#notes` or `#scope` to the app's link.

## Scoring and priorities

ISACA doesn't set a scoring method; the rules below were added for this tool, following common GRC practice. They match the Excel workbook exactly.

**Status and score**

| Status | Score | Meaning |
|---|---|---|
| Implemented | 1.0 | In place, operating and evidenced. |
| Partially implemented | 0.5 | Covers only some agents, tools or environments, is undocumented, or has no evidence it operates. |
| Not implemented | 0 | Absent. |
| Not applicable | — | Left out of scoring. Record why in Gap / observations. |

**Coverage** = (Implemented + 0.5 × Partial) ÷ (Implemented + Partial + Not implemented). Not-applicable and unassessed controls don't count.

**Maturity (0–5):** 0 Non-existent · 1 Initial · 2 Repeatable · 3 Defined · 4 Managed · 5 Optimized.

**Gap priority**

| Priority | Rule |
|---|---|
| P1 | High criticality and Not implemented |
| P2 | High criticality and Partial, or Medium criticality and Not implemented |
| P3 | Any other gap |

Each control comes with a suggested criticality. Change it for a given agent in the control's details to reflect how much damage that agent could do; a read-only summarizer and an agent with write access to production deserve different levels. An overridden criticality is marked with `*`.

**Secure by Default checklist:** an item is **Met** when its linked controls reach 100% coverage, **Partially met** at 50–99%, and **Not met** below 50%. An item with no assessed controls shows **Not assessed**.

## Notes

| Level | Where | Good for |
|---|---|---|
| Control | **Notes** field in a control's details | Context that isn't a gap or remediation step: who you spoke to, caveats, links. Controls with notes show a **Notes** tag. |
| Category | **Add category note** above each category on Controls | Evidence or context shared by every control in the category. |
| Assessment | **Notes** tab | A dated log of interviews, decisions, scope changes and follow-ups. Each entry records the date, time and an optional author name, and can be edited (marked as edited) or deleted (after a confirmation). Ctrl/⌘ + Enter adds a note. |

## Saving and storage

Changes save automatically about a second after you stop typing. The status beside the buttons shows where they went:

| Status | Meaning |
|---|---|
| ● **Saved to this page** (green) | Stored with the page. Available on any device and to anyone you share the page with. |
| ● **Saved in this browser only** (amber) | The page couldn't reach its storage, so your changes are kept in this browser only. A banner explains why and what to do. |
| ● Red message | Something went wrong. The message says what happened and what to do next. |

**When the page can only save in this browser**

| Banner | What to do |
|---|---|
| *Saving to this page needs your permission* | Click **Allow saving**. Saving switches over as soon as you accept. |
| *Saving to this page is turned off for you* | Click **Open permissions** and turn saving back on. If the panel doesn't open, use the page's Permissions menu. |
| *Saving is allowed now. Reload the page* | Reload. Your changes in this browser are kept. |
| *This copy isn't open inside claude.ai* | Open the page from claude.ai or the Claude app. |
| *This view can't reach the page's storage* | Sign in to claude.ai and reopen the page. A signed-out visitor or public link can't save with the page. |

**Moving work out of this browser:** when the page can save and finds assessments kept only in this browser, it lists them by name with a **Move to this page** button. Each one is copied into the page's storage first and removed from the browser only after that copy succeeds. **Not now** hides the banner until the next visit.

If permission is withdrawn while you're working, your unsaved edits switch to this browser and a banner tells you, so nothing is lost.

## Sharing and access

The page is private until you share it from its Share menu. Everyone you share it with sees the same assessments.

| Access level | Can do |
|---|---|
| Owner, Editor | Everything |
| Contributor | Create, edit, import and delete assessments |
| Commenter, Viewer | Read only: inputs are disabled and a banner explains why |
| Signed-out visitor | Nothing is stored with the page; any work stays in their own browser |

Changes are last-writer-wins: if two people edit the same assessment at the same moment, the last save wins. Coordinate on who is editing which assessment.

## Import and export

| Button | Produces | Contains |
|---|---|---|
| **Export CSV** | `AI-agent-assessment-<agent>.csv` | A few rows of assessment details, then one row per control. Category notes, the notes log, checklist overrides and data handling are **not** included. |
| **Export JSON** | `AI-agent-assessment-<agent>.json` | Everything: scope, every control, all notes, checklist overrides and data handling. Use it for backups and to move assessments between copies of the app. |
| **Import** | — | Takes `.csv` or `.json` files, or drop a file anywhere on the page. The type is detected automatically. |

In claude.ai, exports ask you to confirm the download. Where downloads aren't available, the file's contents are copied to the clipboard instead.

**Import always shows a preview first**, with the controls found, status counts and warnings for anything that was skipped. Then you choose:

| File | Options |
|---|---|
| CSV | **Create new assessment**, or **Update** the current one. Update replaces only the controls listed in the file (a control whose row is blank in every field is cleared) and leaves everything else alone. |
| JSON, one assessment | **Create new assessment**, or **Replace** the current one completely. |
| JSON, several assessments | **Create N new assessments** (up to 50 per file). |

**From the Excel workbook:** open the workbook's **Assessment** tab, save it as CSV, and import it.

## File formats

### CSV

Columns are matched by header name, so their order doesn't matter and extra columns are ignored. Upper/lower case, spaces and punctuation in headers are ignored too, so `Gap / Observations` and `gapobservations` both match. Only **ID** and **Status** are required.

| Field | Accepted headers | Accepted values |
|---|---|---|
| Control ID | `ID`, `Control ID` | `GOV-01` … `RES-04`; unknown IDs are skipped with a warning |
| Status | `Status` | Implemented / Partially Implemented / Partial / Not Implemented / Not Applicable / N/A (also Yes, No, Met, Not met) |
| Maturity | `Maturity`, `Maturity (0–5)` | Whole numbers 0–5 |
| Criticality | `Criticality`, `Suggested Criticality` | High, Medium, Low (saved as an override only when it differs from the suggested level) |
| Evidence | `Evidence`, `Evidence / Artifacts` | Text |
| Owner | `Owner` | Text |
| Gap | `Gap / Observations`, `Gap`, `Observations` | Text |
| Remediation | `Remediation`, `Remediation Action` | Text |
| Notes | `Notes`, `Note`, `Comments` | Text |
| Target date | `Target Date` | `yyyy-mm-dd`, `yyyy/m/d`, `m/d/yyyy` or an Excel date number |

Rows above the header row can carry the assessment details as two-column pairs: `Assessment` (or `Agent`), `Organization`, `Assessor`, `Date`, `Version`, `Description`. The app's own CSV export writes these rows.

Score, Gap Priority, Practice Category, control text and framework references are written on export and ignored on import, because they're calculated or fixed.

### JSON

```json
{
  "format": "ai-agent-assessment",
  "schemaVersion": 1,
  "source": "ISACA Cybersecurity Recommendations for Securing AI Agents (2026)",
  "exportedAt": "2026-10-25T12:00:00.000Z",
  "assessments": [
    {
      "name": "Support triage agent",
      "agent": "Support triage agent",
      "org": "Example Co",
      "desc": "Reads inbound support email; can issue refunds under $100",
      "assessor": "Jane Doe",
      "date": "2026-10-20",
      "version": "Draft v0.3",
      "createdAt": "2026-10-20T12:00:00.000Z",
      "updatedAt": "2026-10-25T12:00:00.000Z",
      "r": {
        "IAM-03": {
          "s": "P", "m": 2, "c": "Medium",
          "ev": "Vault dynamic secrets, 1-hour TTL",
          "ow": "Platform Engineering Lead",
          "gap": "Ticketing tool still uses a static API key",
          "rem": "Move to OAuth client credentials",
          "nt": "Key owner unknown",
          "td": "2026-12-15"
        }
      },
      "ck": { "3": { "o": "Met", "n": "Verified in walkthrough" } },
      "cn": { "GOV": "Register lives in the SEC Confluence space" },
      "notes": [
        { "id": "n-abc123", "at": "2026-10-25T12:00:00.000Z", "by": "Jane", "text": "Kickoff held", "editedAt": "2026-10-25T13:00:00.000Z" }
      ],
      "dh": {
        "Confidential": { "agents": "Support triage agent", "acc": "Conditional", "ctx": "Conditional", "mem": "Conditional", "log": "Redacted only", "ext": "Conditional", "cur": "", "gap": "" }
      }
    }
  ]
}
```

| Key | Meaning |
|---|---|
| `r` | Answers per control. `s` status (`I`, `P`, `N`, `NA`), `m` maturity 0–5, `c` criticality override, `ev` evidence, `ow` owner, `gap`, `rem` remediation, `nt` notes, `td` target date |
| `ck` | Checklist overrides keyed `1`–`15`: `o` the override status (`Met`, `Partially met`, `Not met`, `Not applicable`), `n` the reason |
| `cn` | Category notes keyed by category code (`GOV`, `SDL`, `IAM`, `SEG`, `PID`, `DAT`, `TAPI`, `POL`, `MON`, `SUP`, `RES`) |
| `notes` | The assessment's notes log |
| `dh` | Data handling decisions, keyed by data class name. `acc`, `ctx`, `mem`, `log`, `ext` take `Yes`, `No`, `Conditional` or `Redacted only` |

On import, the app also accepts a bare array of assessments, or a single assessment object. Every value is checked:
- **Dropped:** unknown control IDs, invalid statuses and maturities, and unreadable dates, each with a warning.
- **Shortened:** text longer than the limit is cut to length.
- **Replaced:** IDs for log entries are generated fresh on import.

## Limits

| Limit | Value |
|---|---|
| Size of one assessment | About 240 KB. Past that, the status asks you to shorten some notes. |
| Import file size | 2 MB |
| Assessments per JSON import | 50 |
| Notes log entries per JSON import | 500 per assessment |
| Text field length on JSON import | 4,000 characters (8,000 for notes) |

## Source material and what was added

**From ISACA:**
- **Content:** the 11 practice categories, the 80 controls (Figure 3), the 15 checklist items (Figure 4), and the data classes, examples and baseline handling (Appendix A, Figure 5).
- **Wording:** the controls are lightly rephrased as assessment questions.

**Added for this tool (not part of the ISACA paper):**
- **Scoring:** suggested criticality, the maturity scale, scoring, and the P1–P3 rules.
- **Checklist links:** which controls support which checklist item. ISACA doesn't publish this.
- **Framework references:** the ISO/IEC 42001 Annex A, ISO/IEC 27001:2022 Annex A and OWASP Top 10 for LLM Applications (2025) mappings are indicative. Check them before using them as audit or certification evidence.
- **Data handling starting points:** the suggested Yes/No/Conditional answers and agent-specific controls. Replace them with what your data owner approves.

**Repeated controls:** ISACA repeats some controls across categories (for example, separating reasoning from execution appears under both Secure AI Development and Segmentation). Both copies are kept so each category's score matches the paper. Each control's **See also** field points to the other copy so evidence can be reused.

## Troubleshooting

| Problem | Fix |
|---|---|
| Status says **Saved in this browser only** | Read the banner under the tabs; it names the cause and the fix. See [Saving and storage](#saving-and-storage). |
| An assessment is missing on another device | It was probably saved in one browser only. Open the page in claude.ai in that browser and click **Move to this page**. |
| Buttons are greyed out and the inputs are disabled | You have view-only access. Ask the owner for Contributor or Editor access. |
| Import says there's no "ID" and "Status" header | Use a CSV exported from the app, or the workbook's Assessment tab saved as CSV. |
| Imported dates are blank | Use `yyyy-mm-dd`. The preview lists every date it couldn't read. |
| Export copied text instead of downloading | Downloads aren't available in that view. Paste into a new `.csv` or `.json` file. |
| "Too large to save" | Shorten long notes or remove old log entries, or export JSON and split the work into separate assessments. |

## Version history

| Version | Change |
|---|---|
| 1 | Assessment app: 80 controls, scoring, overview, checklist, data handling, CSV export |
| 2 | CSV import with preview, warnings and drag-and-drop |
| 3 | JSON export and import (full backup; several assessments per file) |
| 4 | Notes per control, per category, and a dated notes log |
| 5 | Saving: permission prompt, clear status, explained browser-only fallback, and moving browser-only assessments into the page |
