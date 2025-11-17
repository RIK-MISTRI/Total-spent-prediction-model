# Total Spent Prediction Model (Ridge Regression)

## 🌟 Project Overview

This project focuses on building a highly accurate regression model to predict the **Total Spent** for a retail transaction. The core challenge in the original dataset was the strong multicollinearity between Price Per Unit, Quantity, and the target variable Total Spent (since $\text{Total Spent} \approx \text{Price Per Unit} \times \text{Quantity}$).

The solution involved a crucial **Feature Engineering** step to address this multiplicative relationship, leading to an exceptionally high-performing and stable **Ridge Regression** model.

## 📈 Final Performance Summary

The model was trained on $70\%$ of the data and evaluated on the remaining $30\%$ (test set).

| Metric | Value | Assessment |
| :--- | :--- | :--- |
| **$R^2$ Score** | **0.9516** | **Outstanding.** The model explains over 95% of the variance in Total Spent. |
| **RMSE** | **$20.64$** | The average prediction error is approximately $\$20.64$. |
| **Average Total Spent** | **$129.65$** | The mean transaction value. |
| **Error Rate** | **$15.92\%$** | The RMSE is only $15.92\%$ of the average Total Spent. |

## 🛠️ Methodology: The Key to Success

The high performance was achieved through three essential data science steps:

### 1. Feature Engineering (The Interaction Term)
The **core problem** of multicollinearity was solved by creating an **Interaction Feature**:

$$\mathbf{\text{Quantity\_x\_PricePerUnit}} = \text{Quantity} \times \text{Price Per Unit}$$

This single feature transforms the non-linear multiplicative relationship into a stable, linear one, as visually confirmed by the scatter plot .

### 2. Data Preprocessing & Encoding
All features were converted to a machine-readable format:

* **Missing Values:** All missing values were imputed using the **mean** (for numeric columns) or the **mode** (for categorical columns).
* **Encoding:** Discount Applied, Location, Payment Method, and Category were converted to numerical representations using a mix of **One-Hot Encoding with `drop='first'`** (for binary features) and **Ordinal Encoding** (for Payment Method and Category).
* **Scaling:** All features were standardized using **$\text{StandardScaler}$**, which is vital for Ridge Regression.

### 3. Modeling and Regularization
A **Ridge Regression** model ($\alpha=0.1$) was chosen to stabilize the coefficients and manage any minor residual multicollinearity.

## 🧐 Final Model Interpretation (Business Insights)

The coefficients show the **relative importance** of each feature due to the prior scaling of $X$.

| Feature | Coefficient | Marginal Impact Interpretation |
| :--- | :--- | :--- |
| **$\text{Quantity\_x\_PricePerUnit}$** | **$90.19$** | **Highest Magnitude.** Confirms this is the primary predictor of Total Spent. |
| **Category** | **$0.34$** | **Positive Impact.** Transactions in higher-coded categories are associated with a slight **increase** in Total Spent, holding other factors constant. |
| **Location** | **$-0.14$** | **Negative Impact.** Purchases in the location encoded as $1$ (likely In-store) tend to have a slightly **lower** Total Spent compared to the other location (Online). |
| **Payment Method** | **$0.10$** | **Small Positive Impact.** Transactions with a higher-coded Payment Method are associated with a minor **increase** in Total Spent. |

## 💻 Repository Structure

The project is structured to allow easy reproduction of the results:

* `retail_store_sales.csv`: The raw dataset.
* **`total_spent_prediction.ipynb`**: The main Jupyter Notebook detailing all steps from data loading, preprocessing, feature engineering, scaling, training, evaluation, and final interpretation.
* `Corelation_heatmap.png`: The initial correlation analysis.
* `model_visualization.png`: The scatter plot validating the interaction feature.
