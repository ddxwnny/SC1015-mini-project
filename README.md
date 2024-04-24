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

<img width="282" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/2c58d549-534a-405a-a05b-f9c8c18348a7">

3. Individual Box plot, Histogram & Violin plot

<img width="454" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/1b92782a-83e8-41fe-b102-e22647eb1228">

<img width="499" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/67db2bd2-a947-44d2-adb4-409805a528ea">

<img width="499" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/827a8d33-23e6-4c66-a2e4-7e2433e5e982">

<img width="499" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/0049ade6-0d68-4af2-b613-2b2c1c1d7069">

<img width="499" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/867ce446-52b0-4161-b2a0-89c969261eda">

<img width="499" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/6522509c-6c57-4955-a15b-daf959f9582d">


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
- **Response variable X:** ```Log GDP per capita```, ```Social support```, ```Healthy life expectancy at birth```, ```Freedom to make life choices``` and ```Positive affect```

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
<img width="274" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/f7dd3fc5-4d19-4f57-942d-320afaa465fd"> <img width="247" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/4f21af75-45d3-4b99-8da8-21716ba0b9bc">

 
- The scatter plot shows consistent spread of datas for both training and testing sets
- This indicates that our model is well-fitted and can generalise well to unseen data

### Univariate Linear Regression
- One predictor variable and One response variable
- The goal is to find a linear relationship between these two variables
- Used to rank the significance of the predictors

#### Results
1. Log GDP per capita & life ladder
<img width="489" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/7e21e7a9-fd67-4e25-91cc-1d80f693ec32">
<img width="467" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/eb27329f-bf13-473e-a7b6-6991b6328c3e">

2. Social Support & life ladder
<img width="467" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/9d7d2225-b354-4737-9ec8-2dac43ec3baa">
![image](https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/164141697/7e748b22-e511-4b79-8175-cbde89e17f54)



3. Healthy life expectancy at birth & life ladder
<img width="462" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/6830f3a6-5b50-4747-91b2-403c070f8324">
![image](https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/164141697/a1afedbf-0959-4e35-9722-c20b9bdcd3ae)


4. Freedom to make life choices & life ladder
<img width="419" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/2e9d98d8-17f4-4511-a556-caf44a012875">
![image](https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/164141697/1bfd93fc-0d8b-43a4-b366-6e8893ae4f32)

 
5. Positive affect & life ladder
<img width="455" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/35250ec6-c03c-474e-b033-fe53995b8217">
![image](https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/164141697/ed7e5995-287f-4a5f-a296-0846d677470f)


#### Metrics used for goodness of fit
1. **Explained Variance (R²):**
    - Measures variance in the dependent variable predictable from the independent variables
    - Higher R² value reduces uncertainty in prediction which increase reliability

3. **[Mean Squared Error (MSE):]**
    - The average squared differences between actual and predicted values
    - Lower MSE indicates higher accuracy in predictions

#### Analysis & ranking
<img width="599" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/2f9a9621-b580-4893-8127-77f217cbf4c1">

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

<img width="435" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/86a0e163-d9bc-407a-a672-fab90aabcbaa">

- comparing using 3 variable using Multivariate Linear Regression
    - There is a consistent spread in the scatter plots for both training and testing sets
    - This consistency indicates that our model is well-fitted and can generalise well to unseen data

#### comparing model performance
<img width="502" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/4eec16b0-b7e7-494f-8b1b-02843e463e90">

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

<img width="407" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/2e408dc9-2238-4c8a-9a83-facb21a821be">
<img width="541" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/7699c277-9eb0-4300-b2af-b01791af403e">


- Best parameters are a learning rate of 0.06, max depth of 7 and n estimators of 100
- The results are consistent with the MSE & explained variance & it is and well fitted

### Tensor Flow
- A framework of machine learning and deep learning models.
- **Tensor:** A multidimensional array
- **Flow:** Used to define the flow of data in an operation. It has many hidden layers and neurons to facilitate deep learning and is efficient in handling complex computations

**Results:**

<img width="512" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/45e088c9-6a37-4c3c-af52-8df8c743259d">
<img width="644" alt="image" src="https://github.com/ddxwnny/SC1015_Analysis-of-happiness-index/assets/149656787/66010406-563c-4e28-9b50-2ad22f0bb704">


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


