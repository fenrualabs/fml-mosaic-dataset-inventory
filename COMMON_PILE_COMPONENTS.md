# Common Pile v0.1 — Detailed Component Inventory

**Source Collection:** https://huggingface.co/collections/common-pile/common-pile-v01-raw-data-6826b454a5a6a445d0b51b37  
**Overall:** 8 TB of public domain + openly licensed text from 30 curated sources. Ideal license-safe core for FML-Mosaic-527B.  
**Paper:** https://arxiv.org/abs/2506.05209  
**Filtered version also available.**

This is a deep breakdown of the individual datasets/sources within the raw collection (approximate document counts from HF collection metadata as of latest crawl). All are intended to be public domain or openly licensed.

## Full List of Components

| Dataset Name | Approx. Size (docs/examples) | Link | Notes / Category |
|--------------|------------------------------|------|------------------|
| wikiteam | 552M | https://huggingface.co/datasets/common-pile/wikiteam | Wikimedia dumps / wiki content |
| wikimedia | 78.1M | https://huggingface.co/datasets/common-pile/wikimedia | Wikimedia |
| cccc | 61.6M | https://huggingface.co/datasets/common-pile/cccc | (likely Common Crawl related / cleaned) |
| biodiversity_heritage_library | 45.6M | https://huggingface.co/datasets/common-pile/biodiversity_heritage_library | Biodiversity literature |
| github_archive | 30.4M | https://huggingface.co/datasets/common-pile/github_archive | GitHub-related archives |
| stackexchange | 30.4M | https://huggingface.co/datasets/common-pile/stackexchange | Stack Exchange Q&A |
| uspto | 16.2M | https://huggingface.co/datasets/common-pile/uspto | US patents |
| peS2o | 6.28M | https://huggingface.co/datasets/common-pile/peS2o | Scientific papers (Semantic Scholar / peS2o) |
| caselaw_access_project | 5.52M | https://huggingface.co/datasets/common-pile/caselaw_access_project | Legal case law |
| pubmed | 5.33M | https://huggingface.co/datasets/common-pile/pubmed | Biomedical literature |
| data_provenance_initiative | 4.76M | https://huggingface.co/datasets/common-pile/data_provenance_initiative | Provenance-focused data |
| usgpo | 3.75M | https://huggingface.co/datasets/common-pile/usgpo | US Government Publishing Office |
| arxiv_abstracts | 2.54M | https://huggingface.co/datasets/common-pile/arxiv_abstracts | arXiv abstracts |
| youtube | 1.13M | https://huggingface.co/datasets/common-pile/youtube | YouTube transcripts / related |
| stackv2 | 5.93M | https://huggingface.co/datasets/common-pile/stackv2 | Stack-related (code/Q&A) |
| arxiv_papers | 317k | https://huggingface.co/datasets/common-pile/arxiv_papers | Full arXiv papers |
| news | 172k | https://huggingface.co/datasets/common-pile/news | News sources |
| library_of_congress | 135k | https://huggingface.co/datasets/common-pile/library_of_congress | LOC digitized materials |
| pre_1929_books | 134k | https://huggingface.co/datasets/common-pile/pre_1929_books | Pre-1929 public domain books |
| pressbooks | 107k | https://huggingface.co/datasets/common-pile/pressbooks | Open educational books |
| regulations | 225k | https://huggingface.co/datasets/common-pile/regulations | Regulatory texts |
| project_gutenberg | 73.5k | https://huggingface.co/datasets/common-pile/project_gutenberg | Project Gutenberg books |
| libretexts | 62.3k | https://huggingface.co/datasets/common-pile/libretexts | Open textbooks |
| ubuntu_irc | 329k | https://huggingface.co/datasets/common-pile/ubuntu_irc | IRC logs |
| uk_hansard | 51.6k | https://huggingface.co/datasets/common-pile/uk_hansard | UK parliamentary records |
| doab | 474k | https://huggingface.co/datasets/common-pile/doab | Directory of Open Access Books |
| foodista | 72.1k | https://huggingface.co/datasets/common-pile/foodista | Food/cooking content |
| oercommons | 9.34k | https://huggingface.co/datasets/common-pile/oercommons | Open educational resources |
| public_domain_review | 1.41k | https://huggingface.co/datasets/common-pile/public_domain_review | Public Domain Review |
| python_enhancement_proposals | 656 | https://huggingface.co/datasets/common-pile/python_enhancement_proposals | PEPs (code/docs) |

**Notes:**
- Document counts are approximate from collection metadata and may represent rows or individual documents.
- Many are high-quality domain-specific (legal, scientific, patents, books, wiki, code-related).
- Perfect for mixing into a diverse pretraining corpus while staying license-safe.
- Filtered/deduplicated versions of the overall mix are also available in the related collection.
- Access via Hugging Face Datasets library or direct download. Streaming recommended for large ones.

**Recommendation:** Prioritize mixing these (especially arXiv, peS2o, PubMed, patents, books, StackExchange, Gutenberg) with FineWeb / The Stack for the FML-Mosaic base.

See main [DATASET_INVENTORY.md](DATASET_INVENTORY.md) for overall recommendations and other corpora.
