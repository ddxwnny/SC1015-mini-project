# Analysis of happiness index
We came across a Straits Time article that states that almost 9 in 10 Singaporeans reported feeling stressed in 2023, and 16 per cent said they felt that the stress was "not manageable", according to a new study by a global health firm.

However, based on United Nation World Happiness Report 2024, Singapore was crowned the happiest country in Asia for the second year in the row and ranked 30th globally. Curious about how we achieved this even with our fast-paced lifestyle and stressful environment, we decided to explore further.

## Contributers
1. Dawn Yap Shi Min ([@ddxwnny](https://github.com/ddxwnny)) - Problem Statement, Data Cleaning, Exploratory Data Analysis (Univariate Linear Regression)
2. Ng Yun Fei Aries ([@ariessssx](https://github.com/ariessssx)) - Exploratory Data Analysis (Multivariate Linear Regression), XGBoost 
3. Ong Beng Soon ([@ongbengsoon](https://github.com/ongbengsoon)) - XGBoost, Tensor Flow

## Models used
1. Multivariate Linear Regression
2. Univariate Linear Regression
3. XGBoost
4. Tensor Flow

## About the project
1. [Problem Statement](#problem-statement)
2. [Data Cleaning](#data-cleaning)
3. [Exploratory Data Analysis](#exploratory-data-analysis)
4. [Machine Learning](#machine-learning)
5. [Conclusion](#conclusion)

## Problem Statement
- What are the factors that plays the biggest role for happiness?
- How can the Singapore Government ensure a happy nation?

## Data Cleaning
1. correcting data type
   <img width="285" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/c6bbb90a-943f-4014-a8fe-14e7c42553cd">

  - we corrected the data type for ```year``` & changed it from int64 to category
    
2. replacing NULL values
   <img width="282" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/7d624f59-75dc-4ccc-9be9-ae17d11d81d4">

  - we replaced all the NULL values with median values
    - As compared to 'Mean', Median is more likely to preserve the underlying distribution without skewing to the outliers. this also  preserve integrity of data set, where measure of central tendency is crucial
   
3. Abstract relevant variables
  - ```cleanData```:
    - Life ladder
    - Log GDP per capita
    - Social Support
    - Healthy Life expectancy at birth
    - Freedom to make life choices
    - Generosity
    - Perceptions of corruption
    - Positive affect
    - Negative affect

## Exploratory Data Analysis
1. Heatmap
2. Individual Box plot, Histogram & Violin plot

### Our observations
- From the respective box plots, there are quite a number of outliers in all variables
- We retrieved the count of outliers to determine if it is safe to delete them
- The number of outliers is only a small proportion of the dataset in the variables respectively, it is safe for us to remove this outliers without affecting distribution significantly.
- Some rows have more than 1 variable that is an outlier, thus the sum of all the outliers of individual variables is 105, but there is only a reduction of 89 rows

## Machine Learning
### Multivariate Linear Regression
- Essential for handling multiple predictors and understanding their collective impact on the dependent variable. 
- We assume direct linear relationship.
- As predictors vary, the dependent variable changes directionally.

- **Response variable Y:** ```Life Ladder```
- [Response variable X:](https://github.com/ddxwnny) ```Log GDP per capita```, ```Social support```, ```Healthy life expectancy at birth```, ```Freedom to make life choices``` and ```Positive affect```

- Splitting the Data sets:
    - ```test_size```: 0.2
        - allocating 20% for testing
        - allocating 80% for training
    - ```random_state```: 50
        - ensure reproducible splits& prevent overfitting
     
- ```LinearRegression()``` function used
    - Trained using the ```fit()``` method to learn data patterns
    - Once trained, we use ```predict()``` to estimate the ```Life Ladder``` variable for both training and testing data

#### Model performance: Training VS Testing
- The scatter plot shows consistent spread of datas for both training and testing sets
- This indicates that our model is well-fitted and can generalise well to unseen data

### Univariate Linear Regression
- One predictor variable and One response variable
- The goal is to find a linear relationship between these two variables
- Used to rank the significance of the predictors

#### Results
1. Log GDP per capita & life ladder
2. Social Support & life ladder
3. Healthy life expectancy at birth & life ladder
4. Freedom to make life choices & life ladder
5. Positive affect & life ladder

#### Metrics used for goodness of fit
1. **Explained Variance (R²):**
    - Measures variance in the dependent variable predictable from the independent variables
    - Higher R² value reduces uncertainty in prediction which increase reliability

3. [Mean Squared Error (MSE):](https://github.com/ddxwnny)
    - The average squared differences between actual and predicted values
    - Lower MSE indicates higher accuracy in predictions

#### Analysis & ranking
- Similar "Train" and "Test" MSE: Model is not overfitting

1. Log GDP per capita
2. Healthy Life Expectancy at Birth
3. Social Support
4. Freedom to make life choices
5. Positive affect

#### Refinement to the Multivariate Linear Regression model
**Step:** Isolate and focus on the three key predictors for the next iteration of the model.
**Objective:** To see if refining the model helps to improve the prediction accuracy. 

- **Key predictors identified:**
  1. Log GDP per capita
  2. Healthy Life Expectancy at Birth
  3. Social Support

- comparing using 3 variable using Multivariate Linear Regression
    - There is a consistent spread in the scatter plots for both training and testing sets
    - This consistency indicates that our model is well-fitted and can generalise well to unseen data

#### comparing model performance
- After the removal of “Freedom to make life choices” and “Positive affect”, the linear regression model fair worse
    - This is indicated by an increase in MSE (Test and Train) and a decrease in Explained Variance (Test and Train)
- **Final decision:**
  - We will continue to use all 5 variables when applying other machine models to ensure better performance

### XGBoost
- Utilizes gradient-boosted decision tree
- Similar to the Random Forest
- Combines multiple machine learning algorithms to obtain a better model
- Combine a single weak model with other weak models to make a single strong model which allow for more accurate prediction.

**Results:**
- Best parameters are a learning rate of 0.06, max depth of 7 and n estimators of 100
- The results are consistent with the MSE & explained variance & it is and well fitted

### Tensor Flow
- A framework of machine learning and deep learning models.
- **Tensor:** A multidimensional array
- **Flow:** Used to define the flow of data in an operation. It has many hidden layers and neurons to facilitate deep learning and is efficient in handling complex computations

**Results:**
- The results are consistent with the MSE & explained variance & it is and well fitted

## Conclusion
### Overall results
<img width="644" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/164142416/67266b0a-e35c-4ff0-a55d-48f88508894a">

Overall, XGBoost performed the best for MSE and explained variance, making it the best model for predicting happiness

#### Important determinants
1. Log GDP per Capita
2. Social Support
3. Healthy life expectancy at birth

#### Best model
**XGBoost**

#### Recommendations for the Singapore Government
**Prioritise on:**
1. Log GDP per Capita
   - Maintaining a healthy economy 
2.  Social Support
   - Creating a vibrant community and encourage kindness within the society 
3. Healthy life expectancy at birth
   - Provide affordable healthcare
   - Ensure babies & children get the vaccines they need

- When analysing data collected from Singaporeans, they should use XGBoost for a better result


