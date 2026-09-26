# BITS Pilani Digital – Advanced Grading Console
### CodeForge V1.0: Debug. Reimagine. Deploy.

> **Submission for BITS Pilani Digital CodeForge Challenge V1.0**  
> **Student ID:** `2026eb1100208` | **Email:** `2026eb1100208@bitspilani-digital.edu.in`  
> **Live Production Deployment:** `https://<your-username>.github.io/bits-grading-console/`

---

## 🌟 Executive Overview
This application is an institutional-grade, zero-dependency relative grading console built to model the **BITS Pilani Academic Handbook & Examination Division relative grading regulations**. It resolves 8 critical bugs found in the starter template, preserves 100% of the locked architectural constraints, and introduces 5 high-impact academic enhancements designed specifically for BITS faculty and evaluators.

---

## 🐛 Complete Bug Fix Ledger (8 Bugs Resolved)

| Bug ID | Component | Defect Description | Root Cause | Engineering Resolution |
| :--- | :--- | :--- | :--- | :--- |
| **BUG-01** | Statistics Panel | Inverted Min/Max display | HTML elements had swapped IDs: `id="min"` under Max, `id="max"` under Min | Re-mapped IDs to `statMin`, `statMax`, `statAvg`, `statStd`, `statGPA` |
| **BUG-02** | Sheet Ingestion | Course options duplication on re-upload | Missing dropdown reset and absence of Set deduplication | Implemented clean dropdown reset and applied `[...new Set(courses)]` |
| **BUG-03** | Canvas Graphics | Divide-by-zero canvas freeze ($\sigma = 0$) | When dataset has zero variance, Gaussian formula divides by $\sigma=0$ | Added zero-variance guard: `if (std <= 0.001) return;` |
| **BUG-04** | Session Clock | 1-second display delay on page load | `setInterval` delays first execution by 1000ms | Synchronously invoked initial clock render on DOMContentLoaded |
| **BUG-05** | File Ingestion | Hardcoded legacy `.xls` restriction | `<input accept=".xls">` blocked modern formats | Expanded to `accept=".xls,.xlsx,.csv"` with drag-and-drop dropzone |
| **BUG-06** | Reset Handler | Double confirmation popup spam | Redundant back-to-back `confirm()` calls in handler | Consolidated into a single clean confirmation dialogue |
| **BUG-07** | Type Safety | String concatenation arithmetic flaws | Excel marks parsed as strings corrupted sorting | Wrapped marks in `Math.round(Number(d["Total Marks"] || 0))` |
| **BUG-08** | CSV Export | Commas in names broke CSV column layout | Unescaped string template interpolation | Implemented RFC 4180 quotation escaping on all fields |

---

## 🚀 Key Enhancements Designed for BITS Pilani

1. **Statistical Gaussian Relative Auto-Grading ($\mu \pm k\sigma$):**
   - Automatically computes class Mean ($\mu$) and Standard Deviation ($\sigma$) and dynamically populates optimal relative grading cutoffs following BITS Pilani's relative grading manual ($A \ge \mu + 1.5\sigma$, $B \ge \mu + 0.5\sigma$, etc.) in one click.
2. **Live BITS 10-Point Class GPA Monitor:**
   - Computes real-time average grade points based on the BITS Pilani 10-point scale ($A=10, A^-=9, B=8, B^-=7, C=6, C^-=5, D=4, E=2$), enabling instructors to instantly verify that the course average is within expected institutional targets (~6.8 to 7.5).
3. **Automated Borderline Review Detection:**
   - Automatically scans and flags students who are $\le 2$ marks away from the next higher grade threshold with a clickable alert badge, streamlining the mandatory pre-finalization answer sheet review process.
4. **Interactive Multi-Cohort Demo Data Ingestion:**
   - Evaluators can test the console in 1 click across realistic cohorts:
     - `CS F111 (Computer Programming - 120 Students)`
     - `MATH F111 (Mathematics I - 80 Students)`
     - `EEE F111 (Electrical Sciences - 60 Students)`
5. **Print-Ready Examination Committee Grade Sheet:**
   - Formatted `@media print` stylesheet allowing professors to export official, formatted grade sheets directly to PDF for the Senate/Examination Committee.

---

## 🛠️ Technical Stack
- **Languages:** Semantic HTML5, Modern CSS3 (Grid & Flexbox), Vanilla JavaScript (ES6+)
- **Graphics:** HTML5 Canvas 2D Context with real-time Gaussian distribution rendering
- **Parsing:** SheetJS (`xlsx.full.min.js`) client-side spreadsheet engine
- **Deployment:** GitHub Pages (Serverless, Zero Configuration)
