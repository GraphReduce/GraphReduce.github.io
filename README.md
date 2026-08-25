# GraphReduce

**Coverage-Preserving LLM Aggregation for E-commerce Review Insights**

[Hao Jiang](https://scholar.google.com/citations?user=jVrbKeUAAAAJ) ·
[Xin Li](https://lixin.ai/) · Yichi Zhang ·
[Weisi Lin](https://scholar.google.com/citations?user=D_S41X4AAAAJ)
Nanyang Technological University, Singapore

**EMNLP 2026, Industry Track — Accepted (Poster)**

📄 [Paper (PDF)](static/paper/graphreduce.pdf) · 🌐 **[Project page](https://graphreduce.github.io/)**

---

Product detail pages carry hundreds or thousands of reviews; the interface can
surface only a handful of insights. A deployed insight system therefore has to
answer two questions at once — *what should the summary say?* and *which reviews
support each displayed insight?*

GraphReduce aggregates review tuples into ranked, canonical product-level insight
clusters while keeping **complete member traceability**: an LLM names and ranks
the clusters, but membership is computed outside the model by graph partitioning
and deterministic set union, so every input tuple lands in exactly one output
cluster.

## Results at a glance

| | GraphReduce | best lossless baseline | flat LLM |
|---|---|---|---|
| recall@10 (Software / Fashion / Baby) | 0.609 / 0.536 / 0.674 | 0.575 / 0.502 / 0.618 | 0.532 / 0.516 / 0.618 |
| coverage | **100%** | 100% | 87.2–95.1% |
| duplicate assignments | **0** | 0 | 51–107 |
| coverage at N ≈ 1,500 | **100%** | — | 22.8% |

Recall gains over `hier_agglom` are significant in all three categories
(paired Wilcoxon, n = 100 products); NDCG differences are within bootstrap
uncertainty, so we report ranking parity rather than a ranking win.

## Project page

The page in this repository is a static site — no build step, no dependencies.

```
index.html                      the page
static/images/teaser.jpg        Figure 1
static/paper/graphreduce.pdf    the paper
.nojekyll                       serve static/ as-is
```

To publish it: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.
It will be live at `https://graphreduce.github.io/`.

## Citation

```bibtex
@inproceedings{graphreduce2026,
  title     = {GraphReduce: Coverage-Preserving LLM Aggregation for
               E-commerce Review Insights},
  author    = {Jiang, Hao and Li, Xin and Zhang, Yichi and Lin, Weisi},
  booktitle = {Proceedings of the 2026 Conference on Empirical Methods in
               Natural Language Processing: Industry Track},
  year      = {2026}
}
```

## Data

All experiments use the publicly released Amazon product reviews
([Hou et al., 2024](https://arxiv.org/abs/2403.03952)), restricted to the
Software, Fashion and Baby Products categories. The corpus is de-identified at
release; we collected no new human data and release only aggregate,
product-level insight clusters.
