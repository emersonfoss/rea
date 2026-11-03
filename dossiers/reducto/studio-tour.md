# Reducto Studio + Office — first-hand surface inventory

Observed 2026-11-02 in a logged-in session (org "rayne"), read-only: nothing run, saved, or uploaded. Full inventory with screenshots is retained in the Rayne workspace (`timothy-completion/files/reducto-studio-tour/INVENTORY.md`); this file is the durable summary.

## Docs (docs.reducto.ai)
Self-description: "the agentic document platform… a complete toolkit for the full document lifecycle, from classification and extraction to editing and workflow orchestration." Structure: Get Started (incl. an **Agent Guide**) · Developer Tools (CLI, MCP Server) · Core Functions (Upload, Parse, Extract, Split, Classify, Edit) · Workflows and Pipelines (Pipelines, Chaining, Async & Webhooks) · per-function Configurations · Version Pinning, Rate Limits, Concurrency Throttle. The Quickstart carries a dedicated "fastest path for coding agents" track (Claude Code / Codex / Cursor) — agents are a first-class interface.

## Studio home
Left nav: Home, Usage, API Keys, Webhooks, Billing; footer: Documentation, Support, Give Feedback, Settings. Body: four module cards — Parse ("Convert documents into structured text, tables, and blocks"), Split ("Segment documents into logical sections, pages, or records"), Extract ("Identify and extract structured fields based on a defined schema"), Edit ("Populate existing documents and forms with provided data") — above a **pipelines list** (owner filter, Created sort, search, list/grid, Create pipeline with keyboard shortcut N). Empty state offers two doors: "Build with Reducto" (API key → code or AI agent) and "Start with a document" (upload or sample, "we'll configure together"). The pipeline is the product's central object.

## Pipeline builder (Parse observed)
Opening a module card creates a pipeline draft: document canvas left (file card; PDF/Images/Spreadsheets; Studio max 1GB), configuration right (Configuration | Results tabs; Formatted | JSON output toggle), processor steps as chips with "+ Add", and a **Get Code** button on every pipeline. Parse configuration observed:
- **r-1 (Preview) toggle, ON by default** for new pipelines.
- **Return Parse Citations** — "Returns bounding boxes for each word and table cell."
- **Enhance (Agentic)** passes, each labeled by the failure it fixes: Figure (chart data extraction); Advanced Chart Agent ($0.06/chart); Table ("misaligned columns, merged cells that didn't parse correctly, or numbers that appear in wrong columns"); Text ("Handwritten text, faded scans, documents with unusual fonts, or when you see garbled characters").
- Summarize Figures — "Always supported with r-1" (forced on). Intelligent Ordering — "Always on with r-1."
- Retrieval section (chunking/embeddings). Run disabled until a file is added.

**Pattern worth copying:** configuration as failure-labeled toggles over one default path, with progressive disclosure. **Pattern worth copying 2:** every pipeline exports to code — the UI is a view over the API, not a separate product.

## Office (reducto.ai/office/legal + ChatGPT plugin listing)
Pitch to legal: **"Your agent redlines. You revise."** A live .docx editor (office.reducto.ai/d/<doc>) that ChatGPT, Claude, or any MCP client can edit — remote MCP server at `https://office.reducto.ai/mcp/app`. Every change is a tracked change with a comment; human reviews like ordinary markup. Shared cursors / live co-editing; pages render to match .docx; tables fully editable. Plugin capability list (v2026.10.28): draft/rewrite/shorten/restructure; find & replace across the document; styles/fonts/spacing/lists; headers/footers/footnotes/endnotes/comments; pictures, text boxes, charts, equations, hyperlinks; form fields/content controls; structure and formatting preserved through editing and export.

## Not yet observed
Extract schema-builder UI; Split and Classify pipeline configurations; a Results view with a processed document (citation viewer). Marked unobserved, not inferred.
