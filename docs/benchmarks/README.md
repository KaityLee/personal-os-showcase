# Benchmarks

Definitions of what will be measured and how results will be reported.

> **No measurements yet.** As of 2026-10-28 (UTC) the system is at Phase 1 (scaffolding). Every value below is intentionally empty. Do not infer performance from this page.

## 1. Reporting rules

Every reported result must include:

| Field | Requirement |
|---|---|
| Measurement date | ISO 8601 date in UTC (for example `2026-12-01`) |
| Unit | Stated explicitly (ms, docs/s, %, USD) |
| Environment | Hardware class and OS family, runtime and database versions, whether models run locally or through an API. No hostnames or addresses. |
| Software version | Version or commit identifier of the system under test |
| Dataset | Synthetic or public corpus; number of documents and chunks; languages (BCP 47) and their proportions. Never private notes. |
| Sample size | Number of queries, runs, or requests behind each figure |
| Method | Warm-up, concurrency, and how the statistic was computed |
| Costs | USD, with the measurement date and the date of the price list used |

Rules: no number without a date and a unit; estimates are labelled as estimates; failed or excluded runs are counted and explained, not dropped silently; results are never cherry-picked from several attempts without saying so.

## 2. Metrics

| Metric | Definition | How to measure | Unit | Report format |
|---|---|---|---|---|
| **Recall@5** | Share of the labelled relevant documents that appear in the top 5 results, averaged over queries. | Build a gold set of queries over an anonymized corpus, each with hand-labelled relevant documents. Run retrieval only (no generation). Compare three configurations: full-text only, vector only, hybrid with RRF. | Ratio, 0–1 (three decimals) | Table: configuration × Recall@5, with query count N, corpus size, languages, date. |
| **P50 / P95 latency** | Median and 95th-percentile time from request to complete response. | Report retrieval-only and full RAG answers separately. Exclude warm-up requests. Record server-side time and client-observed time (over the private network) separately. State concurrency (start with sequential, single client). Percentiles over at least the stated N requests. | Milliseconds (ms) | Table: endpoint × P50 × P95, with N, concurrency, warm/cold, date. |
| **Indexing throughput** | Documents (and chunks) fully indexed per second. | Index a fixed corpus from empty: wall-clock time from first job start to last job finish, divided by document count. Report full reindex and incremental update separately. State the embedding model and whether embedding is local or via API. | docs/s (also chunks/s) | Table: scenario × docs/s × chunks/s, with corpus size, average document size, date. |
| **Wrong-source citation rate** | Share of citations in generated answers that point to a source which does not support the statement. | Sample answers from the gold query set. Automatic check: the cited chunk is not in the retrieved set. Manual check: the cited chunk does not support the claim. Count wrong citations over all citations. | Percent (%) of citations | Wrong / total citations, with number of answers sampled, labelling method, date. |
| **API failure rate and retries** | Share of external model or embedding API requests that fail, and how many retries were needed. | Count requests, failures by class (timeout, HTTP 429, HTTP 5xx, other), retries per request, and whether the retry succeeded. Also report the internal API 5xx rate. Collect over a stated period. | Percent (%) failed; mean and max retries per request | Table: failure class × count × %, with total requests, period (UTC dates), provider class, date. |
| **Cost per question** | Average API cost of answering one question end to end. | Sum input and output tokens (and embedding tokens, if any) per question and multiply by the price list in force on the measurement date. Local-model questions are reported separately; hardware and electricity are excluded and the report says so. | USD per question | `USD 0.0000 per question (mean, P95 USD 0.0000, N=…, model=<id>, measured YYYY-MM-DD, pricing as of YYYY-MM-DD)` |

## 3. Results

| Metric | Value | N | Measured (UTC) | Notes |
|---|---|---|---|---|
| Recall@5 | — | — | — | Not measured yet |
| P50 / P95 latency | — | — | — | Not measured yet |
| Indexing throughput | — | — | — | Not measured yet |
| Wrong-source citation rate | — | — | — | Not measured yet |
| API failure rate and retries | — | — | — | Not measured yet |
| Cost per question | — | — | — | Not measured yet |

When results exist, add one section per measurement run, titled with its date, and keep earlier runs for comparison.

## 4. Privacy and reproducibility

- Benchmarks run on synthetic or public corpora. Query logs, chat history, and embeddings derived from private notes must not be published (see the [disclosure policy](../disclosure-policy.md)).
- Describe the corpus and gold-set construction well enough that someone could rebuild an equivalent one.
- Re-run and re-date a result when the system under test, the dataset, the embedding model, or the model pricing changes.
