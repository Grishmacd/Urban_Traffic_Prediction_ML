# Urban Traffic Prediction and City-wise Analysis (Machine Learning)

This project predicts **Average Daily Traffic Counts** using city and urban traffic-related features. It trains a **KNN Regressor** model, evaluates performance using **R² Score** and **Mean Squared Error**, and categorizes the predicted traffic level as **Low / Medium / High**. It also visualizes **average traffic count by city** using a bar chart.


ML flow covered: **Problem Statement → Selection of Data → Collection of Data → Preprocessing → Train/Test Split → Model Selection → Evaluation Metrics → Prediction Level → Visualization**

---

## Problem Statement

Urban traffic varies across cities and depends on factors like speed, accidents, population, and air quality.  
The goal of this project is to:
- Predict **Average_Daily_Traffic_Counts**
- Classify predicted traffic into **Low / Medium / High**
- Compare cities by their average traffic counts using visualization

**Output:** Predicted daily traffic count + traffic level

---

## Selection of Data

**Dataset Type Used:** Structured tabular dataset (Excel)

File used:
- `Urban_Traffic_Data.xlsx`

**Target column (Prediction):**
- `Average_Daily_Traffic_Counts`

**Features used:**
- `City` (encoded to numeric category codes)
- `Year`
- `Peak_Hourly_Traffic_Volume`
- `Percentage_of_Commercial_Vehicles`
- `Number_of_Road_Accidents`
- `Average_Traffic_Speed_kmh`
- `Air_Quality_Index`
- `Population_Million`

---

## Collection of Data

The dataset is loaded using:
- `pd.read_excel("Urban_Traffic_Data.xlsx")`

---

## Preprocessing

### City Encoding
Since ML models require numeric inputs, the `City` column is converted into numeric category codes:

- `df["City"] = df["City"].astype("category").cat.codes`

This keeps the city information usable in model training.

---

## Dividing Training and Testing

The data is split using `train_test_split`:
- Training set: model learns relationships
- Testing set: model is evaluated on unseen data

Used in code:
- `test_size=0.2`
- `random_state=42`

---

## Model Selection

**Model used:** K-Nearest Neighbors Regressor (`KNeighborsRegressor`)

Configuration used:
- `n_neighbors=5`

Why KNN Regression:
- Predicts using similarity between nearby data points
- Works well when patterns are based on neighborhoods in feature space

---

## Evaluation Metrics (Used in this Project)

This project evaluates regression performance using:
- **R² Score:** how well predictions match actual values (higher is better)
- **Mean Squared Error (MSE):** average squared prediction error (lower is better)

Used in code:
- `r2_score(y_test, y_pred)`
- `mean_squared_error(y_test, y_pred)`

---

## Traffic Level Classification (Low / Medium / High)

After predicting traffic count for one test example, the project assigns a level using dataset quantiles:

- `low = y.quantile(0.33)`
- `high = y.quantile(0.67)`

Classification logic:
- `<= low` → **Low Traffic**
- `> high` → **High Traffic**
- otherwise → **Medium Traffic**

Outputs printed:
- Predicted Traffic Count
- Traffic Level

---

## Visualization (City-wise Average Traffic)

The project also performs a city-level analysis:
- Groups dataset by `City`
- Computes mean of `Average_Daily_Traffic_Counts`
- Plots a bar chart showing average traffic per city (sorted descending)

Plot title used:
- **Average Daily Traffic Count by City**

---

## Main Libraries Used (and why)

1. `pandas`  
   - Loads Excel data, handles columns, grouping, and feature selection.

2. `numpy`  
   - Supports numeric operations and calculations.

3. `matplotlib.pyplot`  
   - Creates the city-wise traffic bar chart.

4. `seaborn`  
   - Imported for visualization support/styling (main plot uses Matplotlib).

5. `sklearn.model_selection.train_test_split`  
   - Splits dataset into training and testing sets.

6. `sklearn.neighbors.KNeighborsRegressor`  
   - Trains the regression model for traffic count prediction.

7. `sklearn.metrics`  
   - Computes evaluation metrics: R² Score and Mean Squared Error.

---

## Output

- Printed model performance:
  - R² Score
  - Mean Squared Error
- Predicted traffic count and traffic level (Low/Medium/High)
- Bar chart showing **Average Daily Traffic Count by City**

---

## Developer
Grishma C.D
