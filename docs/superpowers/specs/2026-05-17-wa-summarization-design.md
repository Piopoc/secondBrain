# WA Course Summarization Design

**Date:** 2026-05-17
**Status:** Approved

## Goal
Transform raw files from the `raw/WA - XX` folders into comprehensive, detailed academic summaries in `summaries/WA/`.

## Scope
- **Input:** All folders in `raw/` starting with "WA - ".
- **Output:** One markdown file per folder in `summaries/WA/`.
- **Requirement:** Complete and detailed explanation of every file's content.

## Process Flow
For each folder `raw/WA - XX`:
1. **Inventory:** List all files in the folder.
2. **Deep Analysis:** Read and analyze every file.
3. **Summary Generation:** Create `summaries/WA/WA - XX.md` with the following structure:
    - `# Analysis of WA - XX`
    - `## Overview`: High-level theme of the folder.
    - `## Detailed File Analysis`: 
        - `### [File Name]`
        - Detailed explanation of contents, key concepts, and importance.
    - `## Synthesis`: How files interconnect.
4. **Verification:** Ensure no files are missed and detail is sufficient.

## Technical Details
- **Directory Creation:** Ensure `summaries/WA/` exists.
- **File Handling:** Use `glob` to find folders and `read` to analyze files.
- **Writing:** Use `write` to create the summary files.

## Quality Standards
- Academic rigor.
- Completeness (no file left behind).
- Clarity and detail.
