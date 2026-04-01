# Moniepoint-Customer-Sentiment-Analysis
This project analyses real customer reviews of the Moniepoint Personal Banking app scraped directly from the Google Play Store. The goal was to surface actionable product insights from unstructured user feedback using Python for data collection and sentiment analysis, and SQL for business intelligence queries.

# Tools:
Python · SQL (BigQuery) · Google Play Scraper · TextBlob  
# Data:
2,000 Google Play reviews · Nigeria · March 2026  
# Type: 
End-to-end data engineering project — scraping → cleaning → sentiment scoring → SQL analysis

# Business Questions Answered
What is the overall sentiment distribution across 2,000 reviews?
How does sentiment correlate with star ratings?
What are users most unhappy about? (complaint pattern analysis)
Which reviews did other users find most helpful — and what do they say?
Do newer app versions improve or worsen user sentiment?

Tech Stack
# Layer	                          Tool
Data Collection	Python            Google-play-scraper
Data Cleaning	Python              Pandas
Sentiment Scoring	Python          TextBlob
Storage & Analysis	              Google BigQuery (SQL)
Documentation	                    GitHub · Notion

# Project Structure
```
moniepoint-sentiment-analysis/
│
├── scrape_reviews.py        # Scrapes 2,000 Google Play reviews
├── sentiment_analysis.py    # Cleans data + scores sentiment
├── moniepoint_reviews_clean.csv  # Final clean dataset (2,000 rows, 10 cols)
├── queries/
│   ├── 01_sentiment_overview.sql
│   ├── 02_sentiment_by_rating.sql
│   ├── 03_complaint_analysis.sql
│   ├── 04_helpful_reviews.sql
│   └── 05_sentiment_by_version.sql
└── README.md
```
Dataset Schema
# Column	                         Type	                          Description
reviewer	                       STRING	                        Google Play username
rating	                          INT	                          Star rating (1–5)
review_text	                     STRING	                        Raw review content
review_date	                      DATE                          Date of review
helpful_count	                    INT	                          Number of users who found the review helpful
app_version	                      STRING	                      App version at time of review
platform	                        STRING	                      Google Play / App Store
sentiment	                        STRING	                      Positive / Neutral / Negative
sentiment_score	                  FLOAT	                        TextBlob polarity score (-1 to +1)
review_month	                    STRING	                      Year-month for trend analysis

SQL Queries
Query 1 — Overall Sentiment Breakdown
```sql
SELECT
    sentiment,
    COUNT(*) AS total_reviews,
    ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER(), 2) AS percentage,
    ROUND(AVG(sentiment_score), 4) AS avg_sentiment_score,
    ROUND(AVG(rating), 2) AS avg_rating
FROM `moniepoint_sentiment.reviews`
GROUP BY sentiment
ORDER BY total_reviews DESC;
```





Tech 
