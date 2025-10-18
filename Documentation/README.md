# Documentation

This folder centralizes written deliverables and visual assets that document the TrustX-Defect project lifecycle. Treat it as the canonical archive for anything that leaves the repository and is shared with advisors, reviewers, or external stakeholders.

## Contents at a glance
| File | Type | Purpose |
| ---- | ---- | ------- |
| 24CSM1R23_August_Project_Progress_Report.pdf | Progress report | Monthly status submitted to institute review panel |
| Udit_Jain_Progress_Report_Aug.pdf | Progress report | Personal milestone tracker for supervisor meetings |
| ProgressDocument.pdf | Progress report | Consolidated summary of weekly updates |
| M.Tech Dissertation monthly progress.pdf | Progress report | Official template capturing risks and mitigation plans |
| 24CSM1R23_Major_Project_Report.pdf | Final report | Comprehensive documentation conforming to institute guidelines |
| Major_Project_Report.pdf | Final report | Alternate export of the main project report (layout tweaks) |
| ProjectReport.pdf | Final report | Early draft retained for traceability |
| 24CSM1R23_Dissertation.pptx | Presentation | Slide deck for mid-term evaluation |
| 24CSM1R23_Dissertation_Final.pptx | Presentation | Final defense slides |
| Plagrism_report.pdf | Compliance | Plagiarism screening output required for submission |
| Major_Project_Report.pdf | Final report | Identical content to `24CSM1R23_Major_Project_Report.pdf` with different formatting |
| calib2.png | Figure | Reliability diagram showing calibration improvements |
| glr2.png | Figure | Histogram of gradient layer relevance (GLR) metrics |
| pipeline.png | Figure | End-to-end workflow illustration used across reports |
| shap_curr.png | Figure | SHAP beeswarm for the current baseline |

## File groups and maintenance guidelines
- **Progress reports**  
  Capture chronological updates. When adding a new report, append the month and year in the filename and update this README with a one-line description of the focus (e.g., dataset integration, calibration experiments). Keep PDFs in chronological order to simplify audits.

- **Final reports**  
  Store only the latest approved versions. If you must keep intermediate drafts, suffix them with `_draftX` and note key differences in this README. Align citation references with files in `Research_Papers/`.

- **Presentations**  
  Slide decks should export to PDF before sharing externally. Retain the PowerPoint files here for editing continuity. Track the most recent rehearsal feedback in a short companion text file if the deck changes significantly.

- **Compliance artifacts**  
  Plagiarism and ethics documents are required for submission packets. Record the tool name, date, and threshold in this README when new compliance checks are performed.

- **Figures**  
  Plot exports referenced in documents. Embed image credits or version notes in the plot titles where possible. If figures are regenerated, keep older versions in a dated subfolder or delete them after confirming the new plots appear in all dependent documents.

## Recommended workflow
1. Create visualisations in notebooks, export them directly into `Documentation/` with descriptive filenames.
2. When producing a new draft report or slide deck, increment the filename with the date (YYYYMMDD) until a version is approved, then remove the date for the final archive copy.
3. Mirror any external submission (email, LMS upload, conference portal) by storing the exact submitted PDF here to maintain a verifiable record.

## Style and metadata tips
- Populate the document properties (title, authors, keywords) before exporting to PDF to improve searchability.
- Insert page numbers and revision history tables in long-form reports to help reviewers track changes.
- Include figure captions that reference the corresponding datasets or experiments (e.g., "Calibrated using pc1.csv fold 3").
- For presentations, add speaker notes that mention where source notebooks or scripts reside (`src/proposed_approach_implementations/`).

## Version control considerations
- Large binaries can bloat the repository. If a file exceeds 50 MB, consider using Git LFS or publishing it in cloud storage with access details recorded in this README.
- Avoid committing temporary LaTeX auxiliary files or Word autosave copies. Configure `.gitignore` if necessary.
- When replacing an existing file, mention the change in the commit message (e.g., "Update pipeline.png with post-calibration workflow").

## Cross-references
- Quantitative results in the reports should be reproducible using notebooks in `src/current_approach_implementations/` and `src/proposed_approach_implementations/`.
- Literature cited in the documents is stored in `Research_Papers/`. Maintain consistent citation keys between both directories.
- Any dataset preprocessing choices discussed here should match what is described in `dataset/README.md`.
