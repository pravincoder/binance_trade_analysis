# Portfolio Performance Ranking using ML & Deep Learning

## 📌 Introduction
This project analyzes and ranks portfolio performances using financial metrics. It implements three ranking methods:
1. **Weighted Ranking** - A rule-based approach assigning different weights to key metrics.
2. **XGBoost Pairwise Ranking** - Machine Learning-based ranking using XGBoost.
3. **Deep Learning-based Ranking** - A Neural Network model optimized with a pairwise hinge loss function.

---

## Execution Process 
1. Click on "Complete_Analysis_of_diff_RK_models.ipynb".
2. Click on the colab notebook button.
3. In Colab navbar options click on runtime , "Rull all cells".
4. Scroll at the bottom to see the final visualization and conclusion.

## 📊 Data Preprocessing
1. **Read Trade Data**: The dataset (`trades.csv`) contains transaction details for different portfolios.
2. **Feature Engineering**: Convert timestamps, compute ROI, Sharpe Ratio, Maximum Drawdown (MDD), and other key financial metrics.
3. **Grouping by Portfolios**: Aggregate trade-level data into portfolio-level insights.

```python
# Read the trade.csv
df = pd.read_csv('/content/drive/MyDrive/trades.csv')

# Convert time column to datetime format
df["time"] = pd.to_datetime(df["time"])
```

---

## 📈 Weighted Ranking
Assigns weights to key financial metrics and ranks portfolios accordingly.

```python
df_metrics_W["Weighted_Score"] = (
    df_metrics_W["PnL"] * 0.4 +
    df_metrics_W["ROI"] * 0.3 +
    df_metrics_W["Sharpe_Ratio"] * 0.2 +
    df_metrics_W["Win_Rate"] * 0.1
)
df_metrics_W["Weighted_Rank"] = df_metrics_W["Weighted_Score"].rank(ascending=False, method="dense")
df_metrics_W.to_csv("weighted_ranking.csv", index=False)
```

---

## 🤖 XGBoost Pairwise Ranking
Uses XGBoost to train a pairwise ranking model based on portfolio metrics.

```python
params = {
    "objective": "rank:pairwise",
    "eta": 0.1,
    "gamma": 0.1,
    "max_depth": 4,
    "eval_metric": "ndcg"
}
rank_model = xgb.train(params, dtrain, num_boost_round=100)
df_metrics_Xg["ML_Predicted_Score"] = rank_model.predict(xgb.DMatrix(scaler.transform(X)))
df_metrics_Xg.to_csv("ml_direct_ranking.csv", index=False)
```

---

## 🧠 Deep Learning-Based Ranking
A Neural Network model trained with a custom pairwise hinge loss function.

```python
def pairwise_hinge_loss(y_true, y_pred):
    margin = 1.0
    pairwise_diff = tf.expand_dims(y_pred, 1) - tf.expand_dims(y_pred, 0)
    true_diff = tf.expand_dims(y_true, 1) - tf.expand_dims(y_true, 0)
    weight = tf.where(true_diff < 0, 2.0, 1.0)
    loss = tf.reduce_mean(weight * tf.nn.relu(margin + pairwise_diff * tf.sign(true_diff)))
    return loss
```

```python
model.compile(optimizer=keras.optimizers.Adam(learning_rate=0.001), loss=pairwise_hinge_loss)
model.fit(X_train_tf, y_train_tf, epochs=100, batch_size=32, validation_data=(X_test_tf, y_test_tf), verbose=1)
df_metrics_DL.to_csv("deep_learning_fixed_ranking.csv", index=False)
```

---

## 📊 Results & Model Comparisons
The rankings generated by different models are saved in CSV files:
- `weighted_ranking.csv`
- `ml_direct_ranking.csv`
- `deep_learning_fixed_ranking.csv`

These results can be compared to analyze ranking consistency across different approaches.

---

## 🚀 Future Improvements
- Enhancing the deep learning model with attention mechanisms.
- Experimenting with reinforcement learning-based ranking.
- Deploying the ranking system as an interactive web app.

---

## 📜 Conclusion
This project successfully implements **rule-based, machine learning, and deep learning** approaches for portfolio ranking. Each method has its strengths, and further optimizations can improve ranking accuracy.

🔹 **Author**: Pravin Maurya 
🔹 **Technologies Used**: Python, Pandas, XGBoost, TensorFlow, Scikit-Learn

