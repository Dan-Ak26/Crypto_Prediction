# 🧠 Crypto Price Direction Prediction

## 📘 Overview
This project predicts **next-day price direction** (Up/Down) for 8 major cryptocurrencies using machine learning models.  
The analysis was done in **Google Colab** for the Token Metrics internship take-home assessment.

**Cryptocurrencies used:**
- BTC/USDT  
- ETH/USDT  
- SOL/USDT  
- BNB/USDT  
- XRP/USDT  
- ADA/USDT  
- AVAX/USDT  
- DOGE/USDT  

The dataset was pulled directly from **Binance API** using "ccxt".  
Models were trained on technical indicators such as RSI, MACD, SMA, and ATR to predict next-day movement.

---

## ⚙️ Reproduction Steps

### 1. Open in Colab
Click below to open and run the notebook directly in Google Colab:  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Dan-Ak26/Crypto_Prediction/blob/main/Crypto_data_pull.ipynb)

---

### 2. Install Required Libraries
Run this in the first Colab cell:
- python
**!pip install ccxt ta seaborn scikit-learn xgboost**
### 3. Data Collection
Historical OHLCV (Open, High, Low, Close, Volume) data for 8 crypto assets is fetched via the Binance API.

Data is stored in Pandas DataFrames and merged into one dataset for modeling.

Key code:

python
Copy code
import ccxt, pandas as pd
symbols = ['BTC/USDT', 'ETH/USDT', 'SOL/USDT', 'BNB/USDT', 'XRP/USDT', 'ADA/USDT', 'AVAX/USDT', 'DOGE/USDT']
timeframe = '1d'
### 4. Feature Engineering
Technical indicators are added using the ta library:

- RSI (Relative Strength Index)

- SMA5 and SMA20 (Simple Moving Averages)

- MACD and MACD Signal

- ATR14 (Average True Range)

Extra features:

- RSI and SMA gaps

- MACD difference

- Squared returns for non-linear effects

### 5. Model Training and Evaluation
Three models were trained and compared:

- Model	Accuracy	Precision	Recall
- Logistic Regression	52%	0.47	0.68
- Random Forest	53%	0.47	0.66
- XGBoost	50%	0.40	0.50

Each model predicts the next-day price direction based on the engineered features.

Evaluation metrics:

Precision / Recall / F1-Score

Confusion Matrix

Hit Rate (proportion of correct “Up” predictions)

Cumulative Strategy Return (performance of a simple long-only strategy)

6. Statistical Testing
A two-sample t-test was performed to check if predicted “Up” and “Down” days had significantly different next-day returns.

Result:
- p-value = 0.53 → No statistically significant difference found between groups.

7. Visualization
- Visualizations created using Matplotlib and Seaborn:

- Confusion Matrix Heatmap

- KDE Distribution of Returns (Up vs Down)

- Scatter Plot: Model Prediction vs Next-Day Returns

🧾 **Results and Conclusion**

- Logistic Regression achieved the highest recall (0.68) and moderate accuracy (52%).

- Random Forest achieved the highest overall accuracy (53%), performing slightly better than logistic regression.

- XGBoost did not improve results, likely due to limited data.

- The model’s predictive power is slightly above random chance (50%), showing potential but limited reliability.

- Future improvements could include:

- Using longer training windows (180–365 days)

- Adding more advanced indicators or sentiment data

- Applying deep learning (LSTM, Transformer models) for temporal dependencies.


📂 Folder Contents
bash
Copy code
├── Crypto_Prediction.ipynb   # Main Colab notebook
├── README.md                # This file
└── data/                    # Optional: CSVs or cache (if saved)
🧩 How to Reproduce
Clone or fork this repo:

bash
Copy code
git clone https://github.com/Dan-Ak26/Crypto_Prediction.git
Open Crypto_Prediction.ipynb in Google Colab

Run all cells in order (takes ~2–4 minutes)

Review printed metrics, confusion matrix, and visualizations
