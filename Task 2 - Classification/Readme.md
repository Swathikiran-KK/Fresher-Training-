# Titanic Survival Prediction Project

This project aims to build a **classification model** that predicts the survival of passengers on the Titanic. The process followed a clear **machine learning workflow**, which included **data preparation, exploratory data analysis, feature engineering, model development, and performance evaluation**.

---

## Project Workflow

The steps taken to process the data and develop the predictive models are outlined below:

---

### 1. Data Loading and Initial Assessment

The initial phase focused on loading the datasets and performing a preliminary assessment.  

- **Data Loading**: The `train.csv` and `test.csv` datasets were loaded into pandas DataFrames.  
- **Data Assessment**: The datasets' structure, data types, and missing values were examined using functions like `.head()`, `.isnull().sum()`, and `.info()`.  
- This analysis revealed missing values in the **Age, Cabin, and Embarked** columns in the training data, and **Age, Fare, and Cabin** in the test data.  
- Duplicate entries were also checked (**none were found**).  

---

### 2. Exploratory Data Analysis (EDA)

This stage focused on gaining insights into the data through visualization.  

- **Survival by Sex**: Visualized the count of survivors based on sex using a countplot, showing a higher survival rate for females.  
- **Age Distribution by Sex and Survival**: Used a violin plot to show the distribution of age for each sex and how it relates to survival.  
- **Survival by Passenger Class**: Used a bar plot to visualize the survival rate for each passenger class, indicating that passengers in higher classes had better survival rates.  
- **Distribution of SibSp and Parch**: Countplots were used to show the distribution of siblings/spouses and parents/children aboard.  
- **Survival by Embarked Port**: A bar plot showed the survival rate based on the port of embarkation.  

---

### 3. Feature Engineering and Preprocessing

This stage involved creating new features and preparing the data for modeling.  

- **Family Size and Alone**: Created a `Family_Size` feature by summing `SibSp` and `Parch`, and an `Alone` feature to indicate if a passenger was traveling alone.  
- **Handling Missing Age**: Missing 'Age' values were imputed using the **median age for each combination of Pclass and Sex**.  
- **Handling Missing Embarked**: Missing 'Embarked' values in the training set were filled with the **mode** of the column.  
- **Handling Missing Fare**: The missing 'Fare' value in the test set was imputed using the **median fare for the corresponding Pclass** in the training data.  
- **Title Extraction**: Extracted passenger titles from the 'Name' column and grouped rare titles into a **'Rare'** category.  
- **Feature Encoding**: Categorical features (**Title, Sex, Embarked**) were one-hot encoded.  
- **Column Dropping**: Irrelevant columns such as **Name, Cabin, Ticket, and PassengerId** (from the training data) were dropped.  
- **Column Alignment**: Ensured that the training and test sets had the same columns after preprocessing, adding missing columns to the test set and filling with zeros.  

---

### 4. Addressing Class Imbalance (Planned)

The distribution of the **'Survived'** column was checked and found to be **imbalanced** (more non-survivors than survivors).  

While not fully implemented in the executed cells, the plan included using techniques like **SMOTE** to balance the dataset for potentially improved model performance, especially for predicting the minority class.  

---

### 5. Model Development and Evaluation

This stage involved training and evaluating multiple classification models.  

- **Model Selection**: Several models were chosen for their suitability for classification tasks, including **Logistic Regression, Random Forest, Gradient Boosting, SVC, KNeighbors, and Decision Tree**.  
- **Data Splitting**: The training data was split into training and validation sets to evaluate model performance during development.  
- **Hyperparameter Tuning**: `GridSearchCV` was used with cross-validation on the training split to find the optimal hyperparameters for each model based on various scoring metrics.  
- **Model Evaluation**: The tuned models were evaluated on the validation set using metrics such as **Accuracy, Precision, Recall, and F1-Score**. Confusion matrices were also generated to visualize the model performance.  
- **Cross-Validation**: 5-fold cross-validation was performed on the full training dataset using the best estimators to get a more robust estimate of the models' performance and assess their generalization ability.  

---

### 6. Prediction and Submission

The final stage involved making predictions on the test data and generating the submission file.

- **Best Model Selection**: Based on the evaluation and cross-validation results, the tuned **Random Forest model** was identified as a strong performer.  
- **Prediction on Test Set**: The tuned Random Forest model was used to predict the survival status of the passengers in the test dataset.  
- **Submission File Generation**: A `submission.csv` file was created containing the **PassengerId** from the original test data and the predicted **Survived** values.  
