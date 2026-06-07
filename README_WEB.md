[README.md](https://github.com/user-attachments/files/28681508/README.md)
# WEB_ANALYSIS README

This folder contains the main analysis notebook plus the CSV files it reads and produces for the strict AI companionship news analysis workflow.

`WEB_ANALYSIS.ipynb` is the working notebook. The CSV files are the reusable data artifacts: source crawl batches, cleaned combined outputs, and analysis summary tables.

## Folder Structure

- `data/`: source article-level crawl outputs from earlier collection runs
- `combined_outputs/`: merged and cleaned strict-analysis outputs
- root-level CSVs: summary tables created from the strict cleaned corpus

## Shared Schema Notes

- Most files in `data/` are article-level datasets with columns such as `query`, `discovery_source`, `url`, `domain`, `title`, `text`, `content_length`, `topic_relevant`, and VADER sentiment fields (`neg`, `neu`, `pos`, `compound`, `sentiment_label`).
- `combined_outputs/combined_ai_companion_news_cleaned_strict.csv` and `combined_outputs/combined_ai_companion_removed_rows_strict.csv` extend that article-level schema with merge and cleaning fields such as `dataset`, `source_file`, `detected_language`, `was_translated_to_english`, `clean_text`, `analysis_text`, and `removal_reason`.
- Topic export files add topic assignment columns such as `topic_id`, `topic_score`, `best_k`, and `topic_terms`.
- Row counts below reflect the current files in this folder and may change if the notebook is rerun.

## CSV Inventory

### Root-Level Analysis CSVs

| File | Rows | What it is |
|---|---:|---|
| `ai_companionship_lda_k4_k8_scores_strict.csv` | 5 | LDA model comparison table for `K=4` to `K=8`, including perplexity, topic diversity, and combined ranking used to choose the best topic count. |
| `ai_companionship_lda_topic_terms_strict.csv` | 360 | Long-format topic-term table listing the top weighted terms for each topic across each candidate LDA model. |
| `ai_companionship_network_centrality_strict.csv` | 27 | Centrality metrics for the term co-occurrence network, useful for identifying highly connected or bridging terms in the corpus. |
| `ai_companionship_term_frequency_strict.csv` | 20,297 | Term frequency table generated from the strict cleaned corpus after tokenization and stopword filtering. |
| `summary_ai_companionship_news_strict.csv` | 258 | Sentiment summary grouped by `query` and `sentiment_label`, used to compare how search queries map to positive, neutral, or negative coverage. |

### Combined Strict Outputs

| File | Rows | What it is |
|---|---:|---|
| `combined_outputs/combined_ai_companion_news_cleaned_strict.csv` | 503 | Final merged strict corpus kept for downstream analysis. This is the primary article-level dataset used for topic modeling, sentiment aggregation, and network analysis. |
| `combined_outputs/combined_ai_companion_removed_rows_strict.csv` | 6,360 | Audit table of rows excluded during strict cleaning, including duplicate, off-topic, too-short, and other filtered records. |
| `combined_outputs/strict_topic_example_articles.csv` | 18 | Representative example articles for each best-K topic. Useful for manually interpreting what each topic actually contains. |
| `combined_outputs/strict_topic_sentiment_summary.csv` | 13 | Sentiment distribution by topic, including topic article totals, sentiment percentages, and average compound sentiment score. |

### Topic Category Export CSVs

| File | Rows | What it is |
|---|---:|---|
| `combined_outputs/strict_topic_category_exports/strict_topic_category_summary.csv` | 6 | Index of all topic-level export CSVs, including topic id, topic terms, article count, and output path. |
| `combined_outputs/strict_topic_category_exports/strict_topic_1_chatbots_human_health_mental_mental_health_social_emotional_companions.csv` | 171 | Article-level subset for topic 1. Focuses on chatbot, emotional, social, and mental-health-oriented companionship coverage. |
| `combined_outputs/strict_topic_category_exports/strict_topic_2_information_public_intelligence_law_business_access_legal_human.csv` | 121 | Article-level subset for topic 2. Focuses on public, legal, business, access, and human-intelligence framing. |
| `combined_outputs/strict_topic_category_exports/strict_topic_3_children_care_age_home_chatbots_companion_health_home_care.csv` | 37 | Article-level subset for topic 3. Focuses on children, care, age, home, and health-related companionship reporting. |
| `combined_outputs/strict_topic_category_exports/strict_topic_4_health_mental_mental_health_care_real_support_gemini_help.csv` | 48 | Article-level subset for topic 4. Focuses on health, support, care, and mental-health assistance themes. |
| `combined_outputs/strict_topic_category_exports/strict_topic_5_gemini_access_grok_images_online_companion_latest_claude.csv` | 121 | Article-level subset for topic 5. Focuses on model/platform access and product-oriented companion coverage. |
| `combined_outputs/strict_topic_category_exports/strict_topic_6_chat_nsfw_emotional_privacy_image_adult_interactions_offers.csv` | 5 | Small article-level subset for topic 6. Focuses on adult, NSFW, privacy, and emotionally intimate interaction themes. |

### Source Crawl Batch CSVs

All files in `data/` are crawl-stage article datasets. Files with numeric suffixes such as `...1.csv`, `...2.csv`, and so on are additional crawl batches or follow-on collection parts for the same theme.

| File | Rows | What it is |
|---|---:|---|
| `data/ai_chatbot_companion_news_sentiment.csv` | 3,022 | Large source crawl batch centered on AI chatbot and AI companion news coverage. |
| `data/ai_chatbot_companion_news_sentiment1.csv` | 425 | Additional source crawl batch for the AI chatbot and AI companion theme. |
| `data/ai_companionship_news_sentiment.csv` | 1,784 | Main source crawl batch for the broader AI companionship topic. |
| `data/ai_companionship_news_sentiment1.csv` | 187 | Additional AI companionship crawl batch, part 1. |
| `data/ai_companionship_news_sentiment2.csv` | 510 | Additional AI companionship crawl batch, part 2. |
| `data/ai_companionship_news_sentiment3.csv` | 159 | Additional AI companionship crawl batch, part 3. |
| `data/ai_companionship_news_sentiment4.csv` | 140 | Additional AI companionship crawl batch, part 4. |
| `data/ai_companionship_news_sentiment5.csv` | 120 | Additional AI companionship crawl batch, part 5. |
| `data/ai_companionship_news_sentiment6.csv` | 94 | Additional AI companionship crawl batch, part 6. |
| `data/ai_companionship_news_sentiment7.csv` | 169 | Additional AI companionship crawl batch, part 7. |
| `data/ai_companionship_news_sentiment8.csv` | 30 | Additional AI companionship crawl batch, part 8. |
| `data/ai_companion_japan_news_sentiment.csv` | 86 | Region-specific crawl batch focused on Japan-related AI companion coverage. |
| `data/ai_companion_US_news_sentiment.csv` | 137 | Region-specific crawl batch focused on U.S. AI companion coverage. |

## Suggested Use Order

1. Start with `data/` if you need the original crawl-stage source files.
2. Use `combined_outputs/combined_ai_companion_news_cleaned_strict.csv` for most downstream analysis and reporting.
3. Use the root-level summary CSVs for LDA, network, term-frequency, and query-sentiment reporting.
4. Use `strict_topic_example_articles.csv`, `strict_topic_sentiment_summary.csv`, and `strict_topic_category_exports/` when working at the topic level.
