# Used Car Price Prediction Project  

This project aimed to build a **regression model** that would predict the selling price of used cars. The process followed a clear **machine learning workflow**, which included **data preparation, exploratory data analysis, feature engineering, model development, and performance evaluation**.  

---

## Project Workflow  

The steps taken to process the data and develop the predictive models are outlined below:  

---

### 1. Data Cleaning and Preprocessing  

The initial phase focused on ensuring the dataset's quality and usability.  

- **Data Assessment**: The dataset’s structure, data types, and missing values were thoroughly examined using functions like `.info()` and `.isna().sum()`. This analysis showed that some columns meant for numerical data, such as mileage and engine, were incorrectly formatted as object types, and several features contained null values.  
- **Data Type Conversion**: To allow for numerical analysis and modeling, units like "kmpl", "CC", and "bhp" were removed from the mileage, engine, and max_power columns, followed by converting these to the appropriate numeric types. For the torque column, which had inconsistent formatting, a regular expression extracted the main numerical component, enabling its conversion to a numeric type.  
- **Handling Missing Data**: Missing values in the mileage and engine columns were filled in using the median of their respective distributions. For max_power and seats, the median and mode were used to fill in missing values, as these measures are less affected by outliers.  

---

### 2. Feature Engineering and Exploratory Data Analysis (EDA)  

This stage focused on creating new features and gaining insights through visualization.  

- **Feature Creation**: A new feature, `car_age`, was created by calculating the difference between the current year (2025) and the vehicle's manufacturing year. The original year column was then removed.  
- **Distribution Analysis**: The distributions of numerical features (`car_age`, `selling_price`, `km_driven`, `mileage`, `engine`, `max_power`, `seats`) were visualized using histograms to understand their characteristics and identify potential skewness or outliers.  
- **Outlier Management**: Outliers in the selling_price were identified with a box plot and addressed by removing data points outside the Interquartile Range (IQR). This aimed to improve the model's robustness.  
- **Correlation Analysis**: A heatmap visualized the correlation matrix of the numerical features, revealing linear relationships between variables.  
- **Categorical Feature Examination**: The distributions and effects of categorical features (`fuel`, `seller_type`, `transmission`, `owner`) on selling_price were analyzed using count plots and box plots. The distribution of `owner` was also shown with a pie chart.  
- **Relationship Visualization**: A scatter plot explored the relationship between `max_power` and selling_price.  

---

### 3. Data Transformation for Modeling  

Before training the model, the data was transformed to meet the requirements of the chosen algorithms.  

- **Target Variable Transformation**: A logarithmic transformation was applied to the selling_price to reduce the effects of its skewed distribution, which is often helpful for linear regression models.  
- **Categorical Encoding**: Categorical features (`fuel`, `seller_type`, `transmission`, `owner`, `brand`, `model`) were converted into a numerical format through one-hot encoding. The first category for each feature was dropped to avoid multicollinearity.  
- **Feature Scaling**: Numerical features (`car_age`, `km_driven`, `mileage`, `engine`, `max_power`, `seats`) were scaled using StandardScaler to standardize their ranges, which is common for algorithms sensitive to feature scales.  

---

### 4. Model Development and Evaluation  

This phase involved building and assessing the performance of various regression models.  

- **Data Partitioning**: The dataset was split into training and testing sets to enable model training and unbiased evaluation of performance on unseen data.  
- **Model Implementation**: Several regression models were trained:  
  - Linear Regression  
  - Ridge Regression  
  - Lasso Regression  
  - Gradient Boosting Regressor  
  - Support Vector Regressor  
  - Random Forest Regressor  
  - XGBoost Regressor  
- **Hyperparameter Optimization**: RandomizedSearchCV and GridSearchCV were used to tune the hyperparameters of the Ridge and Lasso regression models. RandomizedSearchCV was also used for the Gradient Boosting, Support Vector, and Random Forest Regressors to find the best parameter combinations.  
- **Performance Metrics**: Model performance was evaluated using key regression metrics: Mean Squared Error (MSE), Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), and the R-squared (R2) score on the test set. Cross-validation was also performed to provide a more reliable estimate of model performance.  
- **Comparative Analysis**: The performance metrics of all models were collected in a table and visualized using bar plots for an easy comparison. This helped identify the most effective model.  

---

### Model Performance Summary  

| Model                       | MSE       | RMSE      | MAE       | R2 (Test) | R2 (CV Mean) |  
|-----------------------------|-----------|-----------|-----------|-----------|--------------|  
| Linear Regression            | 3.82e+09  | 61813.04  | 38377.10  | 0.941     | 0.940        |  
| Ridge Regression             | 3.64e+09  | 60294.28  | 38950.19  | 0.941     | 0.940        |  
| Lasso Regression             | 3.82e+09  | 61813.04  | 38377.10  | 0.941     | N/A          |  
| Gradient Boosting Regressor | 6.66e+04  | 258.13    | 44.35     | 0.999999  | 0.999996     |  
| Random Forest Regressor     | 1.66e+05  | 407.63    | 119.08    | 0.999997  | 0.999994     |  
| XGBoost Regressor           | 2.69e+07  | 5182.47   | 3331.70   | 0.999585  | 0.999498     |  
| Support Vector Regressor    | 6.41e+10  | 253214.38 | 203902.24 | 0.010     | -0.008       |  

---
### Evaluation Metrics to Focus On  

For this regression problem, the key metrics to focus on are:  

- **Root Mean Squared Error (RMSE)**: Measures the average magnitude of the errors, providing higher weight to large errors. Lower RMSE indicates better model performance.  
- **Mean Absolute Error (MAE)**: Measures the average absolute difference between predicted and actual values. It is more robust to outliers than RMSE.  
- **R-squared (R2) Score**: Represents the proportion of variance explained by the model. Higher values closer to 1 indicate better performance.  
- **Cross-Validation R2 Mean**: Provides an estimate of model generalization performance over different subsets of the data.  

These metrics together give a comprehensive picture of the model's accuracy and reliability. 

---
### Conclusion  

Based on the evaluation, the **Gradient Boosting Regressor** showed the best performance in predicting used car prices in this dataset. It exhibited the lowest MSE, RMSE, and MAE, along with the highest R2 score.  
