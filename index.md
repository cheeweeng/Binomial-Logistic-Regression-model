## End-of-course project for Regression analysis: Simplify complex data relationships  

Purpose: to predict user churn based on a variety of variables  
Goal: to build a binomial logistic regression model and evaluate the model's performance.

This activity has three parts:

*   1: EDA & Checking Model Assumptions

*   2: Model Building and Evaluation

*   3: Interpreting Model Results

### Import packages needed for building logistic regression models and load the dataset  


### Explore data with EDA  

2
The dataset has 14999 rows and there are 700 missing values in the label column.  
comprise less than 5% of the data, so drop the rows with missing values in the data.
>  # df=df.dropna(subset=['label'])
2.1
Drop the ID column as it is not helpful to build the model. df = df.drop('ID', axis=1)  

2.2

Just by assessing at the quartile values, standard deviation, and max values, columns have max values that are multiple standard deviations above the 75th percentile. This could indicate outliers in these variables:  
sessions
drives
total_sessions
total_navigations_fav1
total_navigations_fav2
driven_km_drives
duration_minutes_drives

### Feature Engineering    

The churn rate correlates with distance driven per driving day in the last month. It might be helpful to engineer a feature that captures this information.
3.

Some values are infinite due to there being values of zero in the driving_days column. Pandas imputes a value of infinity in the corresponding rows of the new column because division by zero is undefined.
The next step is to convert these values from infinity to zero.  

4.
### Impute Outliers  

Earlier, seven of the variables were determined to indicate clear signs of containing outliers. Instead of dropping them from the dataset, impute the outlying values capped at 95th percentile of each column.  

The label column 
