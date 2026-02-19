# AI Programming Foundations Project

A reproducible data workflow analyzing the NYC Airbnb Open Data (2019) dataset. This project demonstrates data ingestion, cleaning, exploratory data analysis, and visualization using Python, Pandas, and Seaborn as part of the Udacity AI Mastery Capstone.

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

Several sources of bias should be considered when interpreting results from this dataset and workflow:

- **Selection bias:** The dataset only captures listings active on the Airbnb platform, excluding other short-term rental platforms (VRBO, Booking.com) and the traditional hotel market. Conclusions about NYC's overall accommodation market are limited.
- **Temporal bias:** This is a single snapshot from 2019 (pre-pandemic). Pricing patterns, neighborhood popularity, and room-type distributions have likely shifted significantly since then.
- **Missing data bias:** Approximately 10,000 listings have no review data. Filling `reviews_per_month` with zero treats never-reviewed listings as equivalent to inactive ones, potentially underrepresenting new or niche listings.
- **Price self-reporting:** Prices are set by hosts and may not reflect actual transaction prices, seasonal discounts, or negotiated rates.
- **Outlier removal:** Removing listings above the 99th percentile and at $0 excludes legitimate ultra-luxury listings and potential free/promotional stays, narrowing the analysis to a specific market segment.

## Future Integration Reflections

- **Machine learning workflow:** The cleaned dataset provides a foundation for supervised regression — predicting listing price from features like borough, room type, availability, and review count. Feature engineering (e.g., distance to landmarks, neighborhood encoding) could improve model performance.
- **Neural network preparation:** Numeric features would require normalization/standardization. Categorical variables (borough, room type) need one-hot encoding. Regularization (dropout, weight decay) would be important given the moderate dataset size.
- **Agentic automation:** An agentic pipeline could automate data ingestion from live Airbnb APIs, monitor for data drift, flag anomalous pricing patterns, and trigger re-analysis when distribution shifts exceed thresholds.
