
# 🏠 Linear Regression — Housing Price Prediction

**Repository:** *Linear Regression Housing*  
**Notebook analysed:** `Linear regression housing.ipynb`

---

## 🎯 Objective
Build an interpretable **Linear Regression model** to predict **housing prices** using property attributes (area, bedrooms, bathrooms, amenities, furnishing status) and extract **business insights** for valuation strategies.

---

## ⚡ TL;DR

- **Dataset:** 545 houses (structured + engineered categorical features)  
- **Model:** Linear Regression (Ordinary Least Squares)  
- **Performance (test set, 30% split, random_state=42):**  
  - **R² = 0.6463** (model explains ~64.6% of price variance)  
  - **MAE ≈ 920,393**  
  - **RMSE ≈ 1,234,107**  
- **Top positive drivers:** `bathrooms`, `airconditioning_bin`, `hotwaterheating_bin`, `prefarea_bin`, `stories`, `basement`  
- **Notable negative effect:** `bin_unfurnished` → unfurnished homes reduce average price.  
- **Business insight:** Structural features & amenities (bathrooms, AC, hot water heating) have the strongest effect; furnishing and premium amenities can materially shift valuations.  

---

## 📊 Dataset & Preprocessing

- **Rows:** 545  
- **Original features:**  
  `price, area, bedrooms, bathrooms, stories, mainroad, guestroom, basement, hotwaterheating, airconditioning, parking, prefarea, furnishingstatus`  

- **Feature engineering:**  
  - Converted categorical features to binary indicators (`mainroad_bin`, `guestroom_bin`, etc.).  
  - One-hot encoded `furnishingstatus` → `bin_furnished`, `bin_semi-furnished`, `bin_unfurnished`.  

- **Final features used (X):**
```

['area', 'bedrooms', 'bathrooms', 'stories', 'parking',
'mainroad_bin', 'guestroom_bin', 'basement_bin',
'hotwaterheating_bin', 'airconditioning_bin', 'prefarea_bin',
'bin_furnished', 'bin_semi-furnished', 'bin_unfurnished']

````
- **Target (y):** `price`  

---

## 📈 Exploratory Data Analysis

- **Area vs Price**  
![Area vs Price](images/Area%20vs%20price.png)

- **Pairplot (relationships & collinearity check)**  
![Pairplot](images/Paiplot%20of%20all%20the%20variables.png)

---

## 🤖 Modeling: Linear Regression

- **Train/Test split:** 70/30  
- **Algorithm:** `LinearRegression` (scikit-learn)  

### Coefficients (top insights)

| Feature               | Coefficient (approx.) |
| --------------------- | --------------------: |
| `bathrooms`           | +1,114,751            |
| `airconditioning_bin` | +685,839              |
| `hotwaterheating_bin` | +616,375              |
| `prefarea_bin`        | +509,192              |
| `stories`             | +417,268              |
| `basement_bin`        | +482,604              |
| `bin_unfurnished`     | **–220,243** (negative impact) |

📌 **Interpretation examples:**  
- Adding a **bathroom** increases price by ~1.11M (holding others constant).  
- **Air conditioning** adds ~685k; **hot water heating** adds ~616k.  
- **Unfurnished homes** reduce value by ~220k compared to furnished/semi-furnished.  

---

## 📊 Model Evaluation

- **R² (test set):** `0.646`  
- **MAE:** `920,393`  
- **RMSE:** `1,234,107`  

### Visual Diagnostics
- **Prediction vs Actual**  
![Prediction vs Actual](images/Prediction%20vs%20actual%20value.png)

- **Residual distribution**  
![Residuals](images/Residual%20count.png)

- **Q-Q Plot (normality check)**  
![Q-Q Plot](images/Probability%20plot.png)

---

## 🧠 Business Insights

1. **Structural features drive value** → Bathrooms, stories, and area strongly influence price.  
2. **Amenities add premium** → AC, hot water heating, and preferred location significantly boost value.  
3. **Furnishing matters** → Unfurnished homes lose market value vs. furnished ones.  
4. **Parking and basement** also contribute positively to valuation.  

---

## ⚠️ Limitations

- Dataset limited to **545 properties** — generalization may be constrained.  
- Errors (MAE ~920k, RMSE ~1.23M) are large in absolute terms due to housing price scale.  
- Possible **multicollinearity** between structural features (e.g., area, bedrooms, stories).  
- Location captured only by `prefarea` binary — richer geospatial data would improve accuracy.  

---

## ▶️ How to Run

1. Clone the repository.  
2. Place `Linear regression housing.ipynb` and `Housing.csv` in the project root.  
3. Install dependencies:  
 ```bash
 pip install pandas matplotlib seaborn scikit-learn jupyter
````

4. Run the notebook:

   ```bash
   jupyter notebook "Linear regression housing.ipynb"
   ```

---

## 📂 Project Files

* `Linear regression housing.ipynb` → Full analysis notebook
* `Housing.csv` → Dataset (545 rows)
* `images/` → Visual outputs

  * `Area vs price.png`
  * `Paiplot of all the variables.png`
  * `Prediction vs actual value.png`
  * `Residual count.png`
  * `Probability plot.png`

---

## 💡 Highlights

* Built and validated a **Linear Regression model** predicting housing prices with **R² = 0.646**.
* Identified **bathrooms, AC, hot water heating, and furnishing** as strongest price drivers.
* Conducted **EDA, feature engineering, residual diagnostics**, and provided actionable valuation insights.
* Tools: Python (`pandas`, `scikit-learn`, `matplotlib`, `seaborn`).

