# 🏏 IPL Sports Analytics

An end-to-end IPL analytics and match-prediction platform combining machine learning and Power BI, built on IPL ball-by-ball and match data from 2008–2024 (1,092 matches, 260,920 deliveries).

![Dashboard Overview](dashboard/screenshots/dashboard_overview.png)

---

## 📌 Overview

This project analyzes IPL data to:
- Predict live match win probability ball-by-ball using machine learning
- Segment batters into performance archetypes using K-Means
- Surface venue and toss trends that affect match outcomes
- Present findings through an interactive 4-page Power BI dashboard

---

## 🎯 Results at a Glance

**Win Prediction — Model Comparison**

| Model | Accuracy |
|---|---|
| Logistic Regression (baseline) | 77.09% |
| **Random Forest** | **81.86%** |
| XGBoost | 79.36% |

Random Forest scored highest on raw accuracy. XGBoost was chosen as the deployed model for the live win-probability simulator because it outputs better-calibrated probabilities (important for a "win %" style dashboard, not just a win/loss label) and scales more efficiently as more features are added. This trade-off — accuracy vs. probability quality — is something I'd weigh differently depending on the end use case.

**Player Segmentation (K-Means, k=4, on strike rate / batting average / total runs)**

| Cluster | Avg Strike Rate | Avg Batting Avg | Representative Players |
|---|---|---|---|
| 0 – Consistent Anchors | 132.3 | 33.2 | V Kohli, S Dhawan, RG Sharma |
| 1 – Lower-Order/Support | 107.8 | 17.3 | NV Ojha, SC Ganguly, Y Venugopal Rao |
| 2 – Balanced Contributors | 129.0 | 24.1 | RA Jadeja, WP Saha, BB McCullum |
| 3 – Power Hitters | 142.2 | 36.3 | V Sehwag, SE Marsh, AD Russell |

**Match insight:** Across all 1,092 matches, the toss winner won the match only 50.7% of the time — statistically no real advantage, a useful myth-buster surfaced in the Venue Analysis view.

---

## 📂 Project Structure

```
IPL-Sports-Analytics/
├── data/
│   ├── matches.csv              # Raw IPL match data
│   ├── matches_clean.csv        # Cleaned dataset used for modeling
│   └── win_predictions.csv      # Model output predictions
├── notebooks/
│   └── ipl_win_prediction_analysis.ipynb
├── dashboard/
│   ├── IPL_Dashboard.pbix
│   └── screenshots/
├── requirements.txt
└── README.md
```

---

## 📊 Dataset

- IPL ball-by-ball (`deliveries.csv`) and match-level (`matches.csv`) data, 2008–2024
- Sources: [Kaggle](https://www.kaggle.com) and [Cricsheet.org](https://cricsheet.org)
- 1,092 matches · 260,920 deliveries

---

## 🧠 Machine Learning Approach

| Model | Purpose | Result |
|---|---|---|
| Logistic Regression | Baseline win prediction | 77.09% accuracy |
| Random Forest | Non-linear pattern recognition | 81.86% accuracy (best) |
| XGBoost | Deployed win-probability model | 79.36% accuracy, used for calibrated probability output |
| K-Means Clustering (k=4) | Batter segmentation | 210 players clustered into 4 archetypes |

**Features engineered for win prediction (2nd innings, ball-by-ball):**
- `runs_left` — target minus cumulative runs scored
- `balls_left` — balls remaining in the innings
- `wickets_left` — wickets remaining
- `current_run_rate` — run rate so far
- `required_run_rate` — run rate needed to win

---

## 📈 Workflow

```
Data Collection → Data Cleaning → EDA → Feature Engineering
→ Model Training & Comparison → Evaluation → Prediction → Dashboard
```

---

## 🖥️ How to Run

```bash
git clone https://github.com/basavarajasuti69/IPL-Sports-Analytics.git
cd IPL-Sports-Analytics
pip install -r requirements.txt
jupyter notebook notebooks/ipl_win_prediction_analysis.ipynb
```

The Power BI dashboard can be opened with Power BI Desktop: `dashboard/IPL_Dashboard.pbix`

---

## 📸 Dashboard Pages

**Overview** — team-wise wins, toss decision split, orange/purple cap leaders, season totals, navigation to sub-pages

![Dashboard Overview](dashboard/screenshots/dashboard_overview.png)

**Player Analysis** — top run scorers and a strike-rate vs. batting-average scatter plot colored by K-Means cluster

![Player Analysis](dashboard/screenshots/player_analysis.png)

**Venue Analysis** — matches and chasing wins per venue, plus the win-probability-vs-runs-left curve from the XGBoost model

![Venue Analysis](dashboard/screenshots/venue_analysis.png)

**Head to Head** — total matches and head-to-head wins by team, and match-share breakdown by winner

![Head to Head](dashboard/screenshots/head_to_head.png)

---

## 🚀 Future Improvements

- Real-time score/win-probability updates via live API integration
- Fantasy team recommendation engine
- Deep learning model (LSTM) for sequential ball-by-ball prediction
- Re-evaluate Random Forest vs. XGBoost trade-off using AUC-ROC and log-loss, not just accuracy

---

## 👨‍💻 Author

**Basavaraj Asuti**
[LinkedIn](#) · [GitHub](https://github.com/basavarajasuti69)

---

⭐ If you found this useful, consider starring the repo.
