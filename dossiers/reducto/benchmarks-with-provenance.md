# Benchmarks — figures with provenance

Rule: a figure may only be quoted together with its provenance class (see README). Classes: vendor-stated / commissioned / competitor-authored / maintainer-reported / independent. Checked 2026-11-02.

## Reducto-invoked benchmarks
- **RD-TableBench** (open, github.com/reductoai/rd-tablebench): Reducto **90.2%** table similarity; best open entry NVIDIA Nemotron-Parse **85.8%** (arXiv 2511.20478, Table 6). *Provenance caveat:* the 90.2 is Reducto's self-published figure repeated by NVIDIA's paper, not independently re-run.
- **LongExtractBench** (micro1): Deep Extract 99.6% precision/recall, 100% coverage. *Provenance:* **commissioned** — micro1's page states Reducto commissioned it and created the methodology; only 50 of 225 documents are public, so the headline is not reproducible.
- **ExtractBench** (arXiv 2607.29677): Reducto Deep Extract grounding ≈81.1% on scanned pages; open Qwen3.6-35B-A3B >92% on scans/handwriting; page-level grounding 92.0% long docs vs 72.6% short. *Provenance:* **competitor-authored** — the paper is by LlamaIndex, whose own product ranks #1 on it. Figures are verbatim from the paper; the "independent" label used in earlier drafts of this dossier's sources is withdrawn (correction, 2026-11-02).
- **RealDocBench:** Reducto Agentic 91.4 ± 1.7 per-field. **GDP.pdf** (Surge): agentic parse context raised frontier-model task success 21.7% → 30.7%.

## Open-parser benchmarks (context for Timothy's parser choices)
- **OmniDocBench v1.6** (published by MinerU's maker, OpenDataLab — note the interest): OXR-1.0 97.03, **TeleOCR 96.91 (overall leader; TableTEDS 96.82 — best table score)**, PaddleOCR-VL-1.6 96.34 (best FormulaCDM 97.53), MinerU2.5-Pro 95.75, GLM-OCR 95.22 (this is its v1.6 figure; its model card cites 94.62 on v1.5), Gemini 3 Pro 92.91, GPT-5.2 86.59. *Correction recorded 2026-11-02:* earlier summaries credited PaddleOCR-VL-1.6 with the best table score; TeleOCR holds it.
- **olmOCR-Bench:** OXR 87.84 (vendor-submitted), Chandra 2 85.8 (Datalab-published), Mistral OCR 85.20 (**self-reported**; a third-party rerun gives 82.8), Surya 2 83.3 (Datalab-published), olmOCR 2 82.4 (maintainer-reported, Ai2 paper — the only maintainer-run figure in this list).
- **Independent reality check:** InduOCRBench / Real5-style degraded-scan evaluations show *all* systems drop sharply on real-world degraded scans. Leaderboard order on clean benchmarks does not transfer automatically; decisions belong on the buyer's own frozen corpus.

## Compute economics (checked 2026-11-02/03)
- H100 SXM on-demand median **$3.92–3.99/GPU-hr** (index medians corroborated); H200 $5.29–6.19. *Unchecked:* B200 median, H100 spot (~$2.04), hyperscaler premium (+75%), +21% YoY — a fetch failed and was not retried; do not quote until re-checked.
- Worked example (arithmetic verified): 1M pages at 2 pages/s = 138.9 GPU-hours ≈ **$550** rented vs **$10,000** at r-1 list. Break-even vs r-1 ≈ 390 pages/GPU-hour.
