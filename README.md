# ParquetSync Hub

#### ☕ Released by Gemini & Volkan Sah
**Created during a morning coffee session fueled by frustration.**
Stashed and functional. This is a clean, automated bridge for people who hate editing binary files but love clean data for their LLM training.

##  Context & Integration
This Hub is part of a larger ecosystem:
* **[Universal AI HUB](https://github.com/VolkanSah/Multi-LLM-API-Gateway):** The gateway where the data is routed.
* **[SmolLM2-customs](https://github.com/VolkanSah/SmolLM2-customs/):** The destination for the custom-trained models using this data (including the `adi` metrics).

##  Architecture & Workflow
The repository follows a strict **Raw-to-Edit-to-Export** flow to ensure data integrity. No JS-bloat, just pure Python/Polars efficiency.

| Directory | Purpose | Handling |
| :--- | :--- | :--- |
| `raw/` | **Source of Truth** | Original `.parquet` files. Read-only for the pipeline. |
| `editable/` | **Working Copy** | Decoupled `.csv` files for easy browser editing. |
| `exports/` | **Production Ready** | Optimized `.parquet` recompiled for training/Hub. |

## The Logic
1. **Ingest:** Drop a new `.parquet` into `raw/`.
2. **Transform:** Manual GitHub Action triggers `polars` to generate a readable CSV in `editable/`.
3. **Human Edit:** Fix typos, adjust `adi_scores`, or prune rows directly in the GitHub Web UI.
4. **Build:** Trigger the export to recompile the binary `.parquet` into `exports/`.

## Tech Stack
- **Engine:** `Polars` (Lightning fast, handles 500MB+ without breaking GitHub Actions RAM).
- **Automation:** GitHub Actions (Ubuntu-latest + Node 24 enforced).
- **Storage:** Git LFS (Mandatory for keeping the repo slim).

## Security & Integrity
- **Scam Protection:** Keeping data binary in `exports/` makes it harder for basic scrapers to crawl your datasets.
- **Noob-Proof:** Schema-aware processing (handles nested data by flattening to strings).

---
###  Dev Notes
* **Initial Code:** Crafted by Gemini from a human idea after some "AI struggles".
* **First Test after Human fixes (16.03.2026):** Export works! Gemini had some bugs, but we fixed them together.
* **Status:** Functional. Ready to feed the SmolLM2 (or your) training loop.
