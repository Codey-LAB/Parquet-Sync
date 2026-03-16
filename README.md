# ParquetSync ☕

A minimalist, automated pipeline for managing and manually correcting binary Parquet datasets via a human-readable CSV bridge.

> [!TIP]
> **The Data-Centric Advantage & Scalability:**
> For compact models like **SmolLM2**, data purity is everything. This workflow allows you to instantly fix hallucinations by editing the CSV and re-exporting, keeping your training data "pure gold" instead of bulk noise.
> While optimized for small, high-quality datasets, this architecture is **fully scalable**. By leveraging `Polars`, the only limit is your processing power. Whether it's 2.5 MB or several GBs: if you can read it, you can fix it. Edit the binary truth through a human-readable bridge.

### What is this tool?

This tool acts as a dedicated interface between machine-efficient binary data (`.parquet`) and the necessity of manual human intervention. It automates the conversion process, flattens nested structures, and recompiles data back into optimized binary files directly within the GitHub ecosystem.

## Utility for Small Training Sets & Custom Metrics (ADI)

When working with compact models (like **SmolLM2-360M**) and specialized logic such as the **AntiDumpIndex (ADI)**, the quality of individual data points is critical.

* **Precision over Volume:** In small datasets, a single incorrect label or score (e.g., wrong ADI priorities) creates immediate model bias. This hub allows you to manually validate and override `adi_score`, `adi_decision`, or prompts.
* **Nested Data Handling:** Complex metric objects (like `adi_metrics` lists) usually break CSV exports. This pipeline automatically flattens them into strings for editing and restores them for storage.
* **Audit Trail:** Every change to your training data is tracked via CSV diffs, providing a transparent history of your dataset's evolution.

## Architecture & Workflow

The system enforces a strict **Raw -> Editable -> Export** flow to protect the integrity of the original data.

| Directory | Content | Function |
| --- | --- | --- |
| `raw/` | Original .parquet files | The "Source of Truth". Read-only for the pipeline. |
| `editable/` | Generated .csv files | Human-readable working copy for the GitHub browser editor. |
| `exports/` | Final .parquet files | Recompiled binary data for training or [AI HUB](https://github.com/VolkanSah/Multi-LLM-API-Gateway) integration. |

### The Process

1. **To-Editable:** Converts Parquet to CSV using Polars. Nested types are cast to strings to ensure CSV compatibility.
2. **Edit:** Manually fix prompts or adjust ADI values directly in the GitHub Web UI.
3. **To-Export:** Triggers the recompilation of the edited CSV back into the `.parquet` format for the [SmolLM2-customs](https://github.com/VolkanSah/SmolLM2-customs/) training loop.

## Tech Stack

* **Polars:** High-performance DataFrame library for minimal RAM overhead in GitHub Actions.
* **GitHub Actions:** Manual workflow control (Workflow Dispatch) for full process oversight.
* **Git LFS:** Tracking for binary datasets in `raw/` and `exports/`.

## License

This project is licensed under the **MIT*.

---

**Credits:**

* **Concept & Architecture:** Volkan Sah
* **Development:** Created during a morning coffee session to support the [Universal AI HUB](https://github.com/VolkanSah/Multi-LLM-API-Gateway) ecosystem.
* **Technical Support:** Code crafted by Gemini 3 Flash based on human blueprints and requirements.

### Change Log

#### [1.0.0] - 2026-03-16

*Fixed by human (Volkan Sah)*

* **[FIX] Workflow & Permission Bypass:** Resolved the 403 error by explicitly defining `contents: write` permissions. No more "read-only" failures when pushing back to the repo.
* **[FIX] Script Stability:** Fixed `sync.py` to handle nested Parquet data (Complex types to Strings). Eliminated the hallucinations where the AI tried to change filenames and paths mid-project.

**[IDEA]**

* **The "Coffee-Spark":** Concept born from a morning session. Gemini provided the micro-solution architecture.
* **Reality Check:** Initial AI-generated workflows and scripts were trashy and required human intervention to actually function in a real-world dev environment.


>  **Current State:** Export works. Infrastructure is solid. Branching logic for the Hub is finalized.
