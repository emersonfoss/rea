# Reducto — products, deployment, pricing

Verified against Reducto's public docs/pricing on 2026-11-02 (docs effective 2026-09-01). Prices are vendor-stated list prices.

## Products
- **Parse** — documents → structured text/tables/blocks with page-relative bounding boxes and confidence. Two generations: the legacy multi-stage pipeline (OCR + layout + post-processing; "agentic" tier adds VLM passes at 2× price) and **r-1** (launched 2026-09-01), a single post-trained full-page VLM doing text/tables/figures/layout/grounding in one pass. r-1 status: **preview, V3-API-only, opt-in** (`settings.model="r-1"`); new Studio pipelines default to it; existing API integrations stay on legacy. Reducto claims −20% parse error vs its own legacy pipeline and up to 6× cheaper (vendor-stated, internal eval). r-1 mini and automatic per-page routing are announced; shipment unverified as of 2026-11-02. No open weights.
- **Extract** — schema-guided JSON with per-value citations (page + bbox + source text + confidence).
- **Deep Extract** (2026-04-06) — agent harness over Extract: extract → verify against source → re-extract until prompt-defined reconciliation criteria pass. Reducto's documented production-beta scale: **"over 28 million fields on documents up to 2,500 pages long"** (launch blog). Larger figures circulating in secondary write-ups (120M fields / 11,000 pages) have no source and are not used here — correction recorded 2026-11-02.
- **Classify** — natural-language categories with criteria; per-criterion reasoning; first 5 pages by default (max 10). Deep Classify = accurate tier.
- **Split** — natural-language split descriptions + `partition_key`. Deep Split (2026-06-03) runs on the Deep Extract harness and returns per-page evidence strings.
- **Edit** — form filling: AcroForm detection or vision on flat forms, checkboxes/dropdowns, overflow routed to appendix pages; a pre-defined `form_schema` runs ≈3× faster.
- **Studio** — web console; pipelines as the central object (see `studio-tour.md`).
- **Office** (2026-10-29) — full-fidelity DOCX/PPTX/XLSX editing inside ChatGPT/Codex: tracked changes, comments, per-redline accept/reject, live formulas. Account-bound; not self-hostable as a product. **Editor** is the licensed embeddable UI/SDK (engine can run in Node inside customer infrastructure). No standalone Generate/Draft API exists. *Unverified:* the claim that the commercial Editor is based on the MIT docx-editor fork — the fork exists; no source states the lineage.
- **Interfaces** — REST API, Python/Node/Go SDKs, CLI, MCP server.

## Pricing (per 1,000 pages, vendor list, eff. 2026-09-01)
| Item | Price |
|---|---|
| Parse r-1 | $10 |
| Parse legacy | $15 (complex/agentic $30) |
| Extract | $20 |
| Deep Extract | $40 |
| Split | $20 / Deep Split $40 |
| Classify | $7.50 / Deep Classify $15 |
| Edit | $60 (prefilled $15) |
| Batch Queue | −20%, 12h SLA — **Parse and Extract only; Deep Extract is NOT batch-eligible** (correction recorded 2026-11-02) |
| Add-ons | Prompted blocks +$5/1k pages; Advanced Chart Agent $0.06/chart |

Concurrency throttles apply on ~10-page batches (US 200/350/500+ by tier).

## Deployment
Hosted SaaS; hybrid VPC; full VPC / on-prem / air-gapped (Kubernetes + Helm + Terraform; public infra repo `reductoai/reducto-onprem-infra`; container ships all proprietary models). On-prem sizing leaks the legacy stack: `yaml-extract` (30B) on 1× H200; `citation` (7B) on H100/H200; vLLM 0.31.0 or SGLang; ONNX detectors + CRNN + Paddle recognition OCR; LiteLLM fast/accurate tiers (GPT-6 / Gemini-3.x defaults). *Unverified:* LibreOffice conversion in the on-prem stack — not found in the deployment docs (checked 2026-11-02). On-prem license pricing is not published. ZDR, SOC 2 Type II, HIPAA BAA, EU residency are offered.

## Parse details worth copying as requirements
30+ file types; 100MB direct upload / 5GB presigned (Studio states 1GB max). Chunks carry two views: `content` (Markdown; tables as Markdown or HTML) and `embed` (natural-language summaries replacing figures/tables). Chunking modes: disabled / variable / page / section. Signatures return as block + bbox only — the image is deliberately not extracted. Documented language list is 60 (marketing claims 100+; cite the doc list).
