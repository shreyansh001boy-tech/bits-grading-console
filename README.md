# BITS Pilani Digital – Advanced Grading Console (CodeForge V1.0)

> **CodeForge V1.0: Debug. Reimagine. Deploy.**  
> A modern, zero-dependency, statistically resilient relative grading console built for BITS Pilani faculty and instructors.

---

## 🌟 Live Demo & Deployment
- **Live Application:** `https://<your-username>.github.io/bits-grading-console/`
- **Submission ID:** `2026eb1100208`
- **Institution:** BITS Pilani Digital

---

## 🐛 Summary of Bugs Fixed
1. **BUG-01 (Min/Max Inversion):** Corrected the swapped HTML IDs that displayed Maximum marks under "Min" and Minimum marks under "Max".
2. **BUG-02 (Stale Course Options & Duplication):** Added dropdown resetting and `Set` deduplication when uploading multiple files.
3. **BUG-03 (Divide-by-Zero Bell Curve Crash):** Added safeguard for datasets with zero variance ($\sigma = 0$) preventing `NaN` canvas freezes.
4. **BUG-04 (1-Second Timer Delay):** Synchronously triggered initial clock render on DOM ready.
5. **BUG-05 (File Type Restriction):** Expanded file input to accept modern `.xlsx`, `.xls`, and `.csv`.
6. **BUG-06 (Double Confirmation Spam):** Consolidated redundant consecutive `confirm()` calls into a single dialogue.
7. **BUG-07 (String-to-Number Type Casting):** Sanitized and cast Excel mark values with `Math.round(Number(...))`.
8. **BUG-08 (CSV Export Escaping):** Added RFC 4180 quotation escaping to prevent broken columns from names containing commas.

---

## 🚀 Top 3 Enhancements
1. **Statistical Gaussian Auto-Grading ($\mu \pm k\sigma$):** 1-click automatic cutoff calculation based on class Mean and Standard Deviation according to BITS relative grading guidelines.
2. **Interactive Student Roster & Live Grade Inspector:** Real-time searchable and filterable table displaying student ID, marks, grade badge, and percentile rank.
3. **1-Click "Load Sample BITS Dataset":** Instant zero-friction demo button populating realistic synthetic course data (`CS F111`, `EEE F111`) with an interactive drag-and-drop file dropzone.

---

## 🛠️ Tech Stack
- Pure Vanilla JavaScript (ES6+)
- Semantic HTML5 & Responsive CSS Grid/Flexbox
- HTML5 Canvas 2D Context (Real-time animated histogram & Gaussian distribution)
- SheetJS (`xlsx.full.min.js`) for client-side spreadsheet parsing
