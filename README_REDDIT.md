# REDDIT_ANALYSIS README

This folder contains the final Reddit analysis notebook and the CSV artifacts it reads and produces for the AI companion Reddit study.

`reddit_analysis.ipynb` is the main notebook. The CSV files in this folder and its subfolders are the reusable datasets and reporting outputs generated around that notebook.

## Folder Structure

- `data/`: raw or near-raw Reddit crawl batches for posts and comments
- `topic_category_exports/`: topic-level subsets exported from the final best-K topic model
- root-level CSVs: cleaned final dataset and summary tables used for sentiment, vocabulary, topic, and network reporting

## Shared Schema Notes

- `data/posts*.csv` files are post-level Reddit exports with columns such as `subreddit`, `post_id`, `title`, `text`, `score`, and `matched_keywords`.
- `data/comments*.csv` files are comment-level Reddit exports with columns such as `subreddit`, `post_id`, `comment_id`, `text`, `score`, and `matched_keywords`.
- `combined_ai_companion_reddit_sentiment_analysis_final.csv` is the final cleaned article-level analysis table. It contains the merged Reddit content plus the sentiment fields `neg`, `neu`, `pos`, `compound`, and `sentiment_label`.
- Topic export files extend the main final dataset with fields such as `topic_id`, `topic_score`, `best_k`, and `topic_terms`.

## Root-Level CSVs

| File | Rows | What it is |
|---|---:|---|
| `combined_ai_companion_reddit_sentiment_analysis_final.csv` | 32,459 | Final cleaned Reddit analysis dataset produced by the notebook after combining source batches, cleaning text, filtering to AI companion content, and scoring sentiment. |
| `summary_ai_companion_reddit.csv` | 99 | Sentiment summary table grouped by subreddit and sentiment label. Useful for comparing emotional tone across communities. |
| `ai_companion_reddit_term_frequency.csv` | 37,665 | Term frequency table generated from the cleaned Reddit corpus after stopword filtering. Used for the word cloud and lexical analysis. |
| `ai_companion_reddit_lda_k4_k8_scores.csv` | 5 | LDA model comparison table for `k = 4` through `k = 8`, including perplexity, topic diversity, and ranking fields. |
| `ai_companion_reddit_lda_topic_terms.csv` | 360 | Long-format table of top topic terms for each tested LDA model and topic number. |
| `topic_example_articles.csv` | 15 | Example rows representing each topic from the final selected LDA model. Useful for manual interpretation of the topic labels. |
| `topic_sentiment_summary.csv` | 15 | Topic-level sentiment summary showing article counts, topic totals, sentiment percentages, and average compound sentiment scores by topic. |
| `sna.csv` | 29 | Centrality table exported from the term co-occurrence network analysis. It contains term-level graph metrics such as degree centrality and betweenness centrality. |

## Topic Category Export CSVs

| File | Rows | What it is |
|---|---:|---|
| `topic_category_exports/topic_category_summary.csv` | 5 | Index of the per-topic export files, including `best_k`, `topic_id`, `topic_terms`, article count, and output path. |
| `topic_category_exports/strict_topic_1_emotional_human_mental_health_self_mental_health_level_safety.csv` | 4,353 | Topic 1 subset from the final best-K model. This topic centers on emotional support, self-related discussion, safety, and mental-health framing. |
| `topic_category_exports/strict_topic_2_love_story_fun_words_play_role_happy_night.csv` | 6,138 | Topic 2 subset from the final best-K model. This topic emphasizes love, stories, playful interaction, and roleplay-oriented discussion. |
| `topic_category_exports/strict_topic_3_subscription_sm_money_pay_haven_dots_issue_devs.csv` | 9,070 | Topic 3 subset from the final best-K model. This topic focuses on payment, subscription, pricing, issue, and developer/platform concerns. |
| `topic_category_exports/strict_topic_4_voice_characters_experience_personality_kin_grok_features_help.csv` | 6,041 | Topic 4 subset from the final best-K model. This topic centers on voice, character experience, personality, features, and product interaction. |
| `topic_category_exports/strict_topic_5_human_love_help_experience_connection_understand_emotional_humans.csv` | 6,857 | Topic 5 subset from the final best-K model. This topic focuses on human connection, understanding, emotional experience, and relationship meaning. |

## Raw Source Batch CSVs

These files are the input batches used to assemble the final Reddit corpus.

### Post Batches

| File | Rows | What it is |
|---|---:|---|
| `data/posts1.csv` | 1,700 | Reddit post crawl batch 1. |
| `data/posts2.csv` | 4,543 | Reddit post crawl batch 2. |
| `data/posts3.csv` | 5,017 | Reddit post crawl batch 3. |
| `data/posts4.csv` | 2,986 | Reddit post crawl batch 4. |
| `data/posts5.csv` | 640 | Reddit post crawl batch 5. |
| `data/posts6.csv` | 5,156 | Reddit post crawl batch 6. |

### Comment Batches

| File | Rows | What it is |
|---|---:|---|
| `data/comments1.csv` | 1,582 | Reddit comment crawl batch 1. |
| `data/comments2.csv` | 22,993 | Reddit comment crawl batch 2. |
| `data/comments3.csv` | 44,993 | Reddit comment crawl batch 3. |
| `data/comments4.csv` | 33,727 | Reddit comment crawl batch 4. |
| `data/comments5.csv` | 1,794 | Reddit comment crawl batch 5. |
| `data/comments6.csv` | 55,370 | Reddit comment crawl batch 6. |

## Suggested Use Order

1. Use `data/` if you need the original source batches before cleaning and filtering.
2. Use `combined_ai_companion_reddit_sentiment_analysis_final.csv` as the main final dataset for most downstream analysis.
3. Use `summary_ai_companion_reddit.csv`, `ai_companion_reddit_term_frequency.csv`, `ai_companion_reddit_lda_k4_k8_scores.csv`, `ai_companion_reddit_lda_topic_terms.csv`, and `sna.csv` for reporting and appendix tables.
4. Use `topic_example_articles.csv`, `topic_sentiment_summary.csv`, and `topic_category_exports/` for topic-level interpretation and evidence tables.
