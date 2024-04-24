#Analysis of happiness index
We came across a Straits Time article that states that almost 9 in 10 Singaporeans reported feeling stressed in 2023, and 16 per cent said they felt that the stress was "not manageable", according to a new study by a global health firm.

However, based on UN World Happiness Report 2024, Singapore was crowned the happiest country in Asia for the second year in the row and ranked 30th globally. Curious about how we achieved this even with our fast-paced lifestyle and stressful environment, we decided to explore further.

## contributers
1. Dawn Yap Shi Min (@ddxwnny) -
2. Ng Yun Fei Aries (@ariessssx) -
3. Ong Beng Soon (@ongbengsoon) -

## Models used
1. Multivariate Linear Regression
2. Univariate Linear Regression
3. XGBoost
4. Tensor Flow

## About the project
1. [Problem Statement](https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/blob/bb57342afc3ac0c0ce384096a41a1321c49b529b/Happiness%20Index.ipynb#L1)
2. [Data Cleaning] ()
3. [Exploratory Data Analysis] ()
4. [Machine Learning] ()
5. [Conclusion] ()

## Problem statement
- What are the factors that plays the biggest role for happiness?
- How can the Singapore Government ensure a happy nation?

## Data Cleaning
1. correcting data type
  - we corrected the data type for ```year``` & changed it from int64 to category
2. replacing NULL values
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

- Response variable Y: ```Life Ladder```
- Response variable X: ```Log GDP per capita```, ```Social support```, ```Healthy life expectancy at birth```, ```Freedom to make life choices``` and ```Positive affect```

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

### Uniivariate Linear Regression
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
1. Explained Variance (R²):
    - Measures variance in the dependent variable predictable from the independent variables
    - Higher R² value reduces uncertainty in prediction which increase reliability

3. Mean Squared Error (MSE):
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

- Key predictors identified:
  1. Log GDP per capita
  2. Healthy Life Expectancy at Birth
  3. Social Support

- comparing using 3 variable using Multivariate Linear Regression
    - Here is the code and scatterplot for the multivariate linear regressions with three predictors. There is a consistent spread in the scatter plots for both training and testing sets. This consistency indicates that our model is well-fitted and can generalise well to unseen data.


   

### XGBoost


### Tensor Flow


## Conclusion





