## End-of-course project for Regression analysis: Simplify complex data relationships  

Purpose: to predict user churn based on a variety of variables  
Goal: to build a binomial logistic regression model and evaluate the model's performance.

This activity has three parts:

*   1: EDA & Checking Model Assumptions

*   2: Model Building and Evaluation

*   3: Interpreting Model Results

### Import packages needed for building logistic regression models and load the dataset  
<img width="758" height="460" alt="Image" src="https://github.com/user-attachments/assets/dd19b2c7-c2c9-4a79-a855-33e7781e3f94" />

### Explore data with EDA  

<img width="450" height="510" alt="Image" src="https://github.com/user-attachments/assets/00ede1f3-3e7f-42a6-80b6-21fafa77a742" />

The dataset has 14999 rows and there are 700 missing values in the label column.  
These comprise less than 5% of the data, so drop the rows with missing values in the data.
>  # df=df.dropna(subset=['label'])  
<img width="750" height="250" alt="Image" src="https://github.com/user-attachments/assets/4b4c9724-6d9a-4929-ad32-14ad6e991782" />

Drop the ID column as it is not helpful to build the model.  
>  # df = df.drop('ID', axis=1)    

<img width="800" height="400" alt="Image" src="https://github.com/user-attachments/assets/b7da8c35-4f21-43b0-b056-387e17997d55" />

Just by assessing at the quartile values, standard deviation, and max values, columns have max values that are multiple standard deviations above the 75th percentile. This could indicate outliers in these seven variables:  
sessions, drives, total_sessions, total_navigations_fav1, total_navigations_fav2, driven_km_drives, duration_minutes_drives

### Feature Engineering    

The churn rate correlates with distance driven per driving day in the last month. It might be helpful to engineer a feature that captures this information.  
<img width="650" height="320" alt="Image" src="https://github.com/user-attachments/assets/a760dd89-f09d-4b30-ae49-c36922b3f98e" />

Some values are infinite due to there being values of zero in the driving_days column. Pandas imputes a value of infinity in the corresponding rows of the new column because division by zero is undefined.
The next step is to convert these values from infinity to zero.  

<img width="650" height="373" alt="Image" src="https://github.com/user-attachments/assets/f6e25918-7163-4316-8a2d-462411c99a8d" />

### Impute Outliers  

Earlier, seven of the variables were determined to indicate clear signs of containing outliers. Instead of dropping them from the dataset, impute the outlying values capped at 95th percentile of each column.  
<img width="862" height="174" alt="Image" src="https://github.com/user-attachments/assets/50b181c4-06bb-4619-9481-8c09b52d2e88" />    

The label column is the target of this analysis and it is a categorical variable which needs to be changed to binary.
This change is needed to train a logistic regression model.  We will assign a 0 for all retained users and a 1 for all churned users.  
6

### Check Assumptions
