# BITS Pilani Digital — CodeForge V1.0 Bug Fix Log

**Student Name:** [Your Name]  
**BITS ID:** 2026eb1100208  
**Programme:** [Your Programme, e.g., B.Tech / M.Tech / Work Integrated Learning Programmes]  
**Application Title:** BITS Pilani Digital – Advanced Grading Console  
**Repository:** https://github.com/[your-username]/bits-grading-console  
**Live Deployed URL:** https://[your-username].github.io/bits-grading-console/  

---

## Tabular Bug Fix Log

| Bug # | Component / Line | Description of Bug | Root Cause Analysis | Fix & Technical Resolution | Verification & Result |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BUG-01** | Statistics Panel<br>(Lines 220–223) | **Inverted Min and Max Values:** Minimum mark displayed under the "Max" header and maximum mark displayed under "Min". | The HTML template assigned `id="min"` to the Max container and `id="max"` to the Min container. JavaScript populated `min` with `m[0]` and `max` with `m[m.length-1]`. | Renamed HTML target IDs to `statMin`, `statMax`, `statAvg`, `statMed` and updated JS mappings accordingly. | Verified with marks [15, 45, 92]. Min shows 15, Max shows 92 correctly. |
| **BUG-02** | File Upload Parser<br>(Lines 312–322) | **Stale & Duplicate Course Options:** Uploading multiple sheets causes courses to duplicate 100+ times without resetting. | `data.map(d=>d.Course).forEach(...)` added options without resetting `course.innerHTML` or deduplicating course names. | Implemented `courseSelect.innerHTML = '<option value="">Select a Course</option>'` and applied `[...new Set(courses)]` deduplication. | Uploaded sheets with 150 rows across 2 courses; dropdown displays exactly 2 unique options. |
| **BUG-03** | Canvas Bell Curve<br>(Lines 425–439) | **Divide-by-Zero Render Crash (`NaN`):** If all students receive identical scores, canvas freezes. | Standard deviation $\sigma = \sqrt{\frac{\sum (x - \mu)^2}{N}} = 0$. The Gaussian formula $\frac{1}{\sigma \sqrt{2\pi}}$ divides by zero, producing `Infinity` and `NaN`. | Added safety guard: `if (std <= 0.001) return;` preventing zero division and gracefully rendering bars without curve crash. | Tested with test dataset where all marks = 75. Canvas renders without console error. |
| **BUG-04** | Session Timer<br>(Lines 275–294) | **Initial 1-Second Timer Lag:** Timer display remains static at "00:00" for the first 1000ms. | `setInterval` executes its callback only after the first delay (1 second) elapses. | Extracted `updateTimer()` and called it synchronously inside `startTimer()` before initiating `setInterval`. | Timer updates instantly on DOM ready without visual freeze. |
| **BUG-05** | File Input Filter<br>(Line 188) | **Modern Excel Rejection:** File picker strictly enforced `.xls`, rejecting standard modern `.xlsx` and `.csv`. | Hardcoded `accept=".xls"` attribute in the file input tag. | Updated attribute to `accept=".xls,.xlsx,.csv"` and wrapped in an interactive dropzone. | Successfully ingested `.xlsx`, `.xls`, and `.csv` files via file picker and drag-and-drop. |
| **BUG-06** | Reset Action<br>(Lines 374–376) | **Double Confirm Dialogue Spam:** Clicking "Reset Range" triggered two consecutive browser popups. | Redundant back-to-back `confirm()` calls in the event handler. | Consolidated into a single explicit confirmation dialogue: `confirm("Reset all grade ranges to standard default values?")`. | Single click resets ranges cleanly without multiple interruptions. |
| **BUG-07** | Data Casting<br>(Lines 393–404) | **String Concatenation Arithmetic Flaws:** Excel numbers parsed as strings caused sorting/filtering inconsistencies. | Lack of explicit numeric casting when accessing `d["Total Marks"]`. | Added `Math.round(Number(d["Total Marks"] || 0))` during data ingestion. | Verified with string numeric values (`"85"`). Properly sorted and categorized into grade bins. |
| **BUG-08** | CSV Export<br>(Lines 472–485) | **CSV Injection / Header Breakage:** Instructor name or course with commas broke CSV column layout. | Unquoted string template interpolation in `csv += ...`. | Added RFC 4180 compliant quote escaping: `"${str.replace(/"/g, '""')}"`. | Exported file with commas in name; columns open perfectly aligned in Excel. |

---

## Top 3 Enhancements Implemented

### 1. Statistical Gaussian Relative Auto-Grading ($\mu \pm k\sigma$)
* **What it does:** Automatically computes the class Mean ($\mu$) and Standard Deviation ($\sigma$) and dynamically populates optimal relative grading cutoffs ($A: \mu + 1.5\sigma$, $A^-: \mu + 1.0\sigma$, $B: \mu + 0.5\sigma$, etc.) following BITS Pilani's relative grading policy.
* **Why it matters:** Eliminates tedious manual guesswork for faculty, guaranteeing a continuous, statistically balanced Gaussian grade distribution in one click.

### 2. Interactive Real-Time Student Inspector & Roster Preview
* **What it does:** Displays an interactive, real-time student table showing BITS ID, Total Marks, assigned Grade badge, and individual class percentile rank. Features real-time search and grade filter pills.
* **Why it matters:** Allows instructors to audit border cases (e.g. students near the A/A- cutoff) instantly before finalizing.

### 3. One-Click "Load Sample BITS Dataset" & Universal Drag-and-Drop Dropzone
* **What it does:** Evaluators and faculty can test the application with a single click using synthetic, realistic BITS course data (`CS F111`, `EEE F111`) without needing to create or find an Excel file. Also supports drag-and-drop file uploading.
* **Why it matters:** Enhances user experience and allows instant zero-friction demonstration.
