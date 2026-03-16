# ParquetSync Hub

#### Idea stashed. Will soon craft it. 
Born out of boredom while Claude was debugging and Gemini was being Gemini. This is a clean, automated bridge for people who hate editing binary files but love clean data.

## Architecture & Workflow

The repository follows a strict **Raw-to-Edit-to-Export** flow to ensure data integrity. No JS-bloat, just pure Python/Polars efficiency.

| Directory | Purpose | Handling |
| :--- | :--- | :--- |
| `raw/` | **Source of Truth** | Original `.parquet` files. Read-only for the pipeline. |
| `editable/` | **Working Copy** | Decoupled `.csv` files for easy browser editing. |
| `exports/` | **Production Ready** | Optimized `.parquet` recompiled for training/WhatsApp/Hub. |

## The Logic
1. **Ingest:** Drop a new `.parquet` into `raw/`.
2. **Transform:** GitHub Action triggers `polars` to generate a readable CSV in `editable/`.
3. **Human Edit:** Fix typos or prune rows directly in the GitHub Web UI.
4. **Build:** On commit, the pipeline validates the schema and builds the final `.parquet` in `exports/`.

## Tech Stack
- **Engine:** `Polars` (Lightning fast, handles 500MB+ without breaking GitHub Actions RAM).
- **Automation:** GitHub Actions (Ubuntu-latest).
- **Storage:** Git LFS (Mandatory for keeping the repo slim).

## Security & Integrity
- **Scam Protection:** Keeping data binary in `exports/` makes it harder for basic scrapers to steal your training sets.
- **Noob-Proof:** Schema validation prevents builds if the CSV structure is mangled.

---
*Status: Stored for later. No code touched yet, just the blueprint.*

> code crafted by Gemini from a human idea after sickness

### Code test
Tested first time. 16.03.2026 - reult, geminie 3 Pro cant code! Will fix it self! But Idea was cool :D 
