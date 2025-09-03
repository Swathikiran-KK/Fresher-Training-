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

### 4. Model Development, Evaluation, and Metrics  

The key metrics to focus on are **Precision, Recall, and F1 Score**.  

- **Precision** measures the accuracy of positive predictions (survivors predicted correctly).  
- **Recall** measures the ability of the model to find all actual survivors.  
- **F1 Score** is the harmonic mean of Precision and Recall, providing a balanced measure.  
- **Accuracy** provides an overall correctness metric but may not reflect class-specific performance fully.  

According to the evaluation metrics and cross-validation results, the tuned **Random Forest model** performed best with the following scores on the validation set:  

- Accuracy: 0.8380  
- Precision: 0.8333  
- Recall: 0.7246  
- F1 Score: 0.7752  
- Cross-Validation Mean Accuracy: 0.8260  

This demonstrates the Random Forest model’s strong predictive capability with balanced performance between identifying true survivors and minimizing false predictions.  

---

### 5. Prediction and Submission  

The final stage involved making predictions on the test data and generating the submission file.  

- **Prediction on Test Set**: The tuned Random Forest model was used to predict the survival status of the passengers in the test dataset.  
- **Submission File Generation**: A `submission.csv` file was created containing the **PassengerId** from the original test data and the predicted **Survived** values.  
