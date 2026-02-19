# AI Programming Foundations Project

A reproducible data workflow analyzing the NYC Airbnb Open Data (2019) dataset. This project covers data ingestion, cleaning, exploratory data analysis, and visualization using Python, Pandas, and Seaborn as part of the Udacity AI Mastery Capstone.

## Dataset

**NYC Airbnb Open Data** — 48,895 short-term rental listings across New York City's five boroughs (2019).

Source: [Kaggle — New York City Airbnb Open Data](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data)

## How to Run

```bash
# Clone the repository
git clone https://github.com/trwilcoxson/ai-programming-foundations-project.git
cd ai-programming-foundations-project

# Install dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook data_workflow.ipynb
```

The dataset (`AB_NYC_2019.csv`) is included in the repository, so the notebook runs immediately after cloning.

## Project Structure

```
ai-programming-foundations-project/
├── data_workflow.ipynb      # Main analysis notebook (6 sections)
├── AB_NYC_2019.csv          # NYC Airbnb dataset (48,895 rows)
├── module_summary.pdf       # Project report (APA format)
├── requirements.txt         # Pinned Python dependencies
└── README.md                # This file
```

## Bias Awareness

The way you clean data has a real effect on what the analysis shows. In this project, a few of my cleaning choices could introduce bias:

- Filling `reviews_per_month` with zero for the ~10,000 listings that had no reviews means I'm treating "never reviewed" and "inactive" as the same thing. New listings or ones in less popular neighborhoods might have no reviews yet, and lumping them in at zero could skew any analysis that relies on review metrics toward older, more established properties.

- Removing $0 listings and everything above the 99th percentile ($799) cuts out both ends of the price range. Some of those $0 entries might be real promotional listings, and some high-priced ones are legitimate luxury stays. Choosing a different cutoff (like 95th or 99.5th percentile) would change the summary statistics noticeably, so this threshold is somewhat arbitrary.

- The dataset itself only covers Airbnb — it doesn't include VRBO, Booking.com, or traditional hotels, so any conclusions are limited to one platform's slice of the market.

- This is a 2019 snapshot taken before the pandemic. Pricing and availability patterns have almost certainly changed since then, so these findings shouldn't be read as current.

- Prices are whatever hosts decided to list, not what guests actually paid. Cleaning can't fix that kind of measurement issue.

## Future Integration Reflections

- **How the workflow would change for ML:** To use this data for machine learning, I'd need to add a train/test split after the cleaning step, do feature selection (the correlation matrix from the EDA gives a starting point), and set up a training and evaluation loop with something like RMSE or MAE for a price-prediction regression task. Borough, room type, availability, and review count would be the main features. I could also engineer new features — like distance to landmarks or a "host experience" score based on listing count — to get better predictions than the raw columns alone would give.

- **What neural networks would need:** Neural networks would need the numeric features (price, minimum_nights, availability_365) normalized to similar scales, and the categorical features (borough, room type) one-hot encoded or turned into embeddings. With only ~48K rows, overfitting would be a real concern, so I'd want to use dropout and weight decay during training. The good news is that the cleaning pipeline already handles nulls and outliers, so the data is in pretty good shape for that next step.

- **Where an AI agent could help:** An agent could handle the repetitive parts of this workflow automatically — pulling new data from an API, checking whether the price distribution or room-type mix has shifted since the last run, and flagging anything unusual. Since the notebook already has separate functions for ingestion, cleaning, and analysis, an agent could call each one in sequence and decide whether the results need human review or can just be logged.
