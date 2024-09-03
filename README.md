BUSINESS UNDERSTANDING:

Background

Pricing is one of the most important parts of success in the sale of any good or product, the used car sales market is no exception.  Price too high, or too low and you will not be able to keep up with the market.  In order to price correctly, a business needs to understand what features of a product drives consumer demand.  

Business Objectives

This project seeks to analyze past used car sales data and decide what features are most important in determining the price of a car.

Business Success Criteria

A model has been developed that can successfully predict the price of a used car within the same population type (demographics) of data that the model was trained under.

Assess Situation

Data available for past car sales in Kaggle will be used.  The constraints and assumptions here is that data is not necessarily global and that it’s predictive power will be limited only to making predictions within a similar demographic.

Determining Data Mining Goals

The data mining goals are to transform the Kaggle data into a numeric set of features that can be used in a linear model.  This involves transforming data into ordinal where needed and being able to convert categorical data into binary or one hot encoded data where needed.

Project Plan

The CRISP process model will be used to create a Model that can be used to predict the price of a used car based on the set of feature determined to have the most impact on car sales.  The project plan will be as follows: Data Understanding, Data Preparation, Modeling, Evaluation and Deployment.  Several models will be tested and evaluated before a final model is selected, so there will be several iterations between the Data Preparation and Modeling phases before each model is evaluated and a final model selected.

DATA UNDERSTANDING:

The data used for modeling and training is from Kaggle. The steps that were taken to analyze the data were as follows:
1.	Read the data in into a data frame using pandas library in Python
2.	Used info() method on the dataframe to find out the column names and what types they were
3.	Used the isNull() method on the dataframe to find out how many columns have null values and the null counts
4.	Used the unique() method on the dataframe to find out the unique values in the key feature fields that are non-numeric
5.	Determined categorical features and discrete data and analyzed what transformations would be needed in subsequent steps.  
6.	Used groupby feature on dataframe to group categorical data and found their mean price in order to see if data was ordinal based on the values and their correlation with the price.
7.	Plotly bar graphs were used to visualize the relationship between the price and other key features such as car condition, car size and number of cylinders.  

Based on the data understanding business research was done to determine what features in the data have historically affected the price of used cars.  This was used as a starting point or hypothesis to determine the subset of features in the data that would be candidates for the prediction model.

DATA PREPARATION: 

During data preparation, null columns were dropped.  The features that were to be tested based on business understanding and research, along with the data understanding were selected into a training set dataframe.  Non-numeric, categorical data and binary data were transformed into numerical data using column transformers (ordinal and one hot encoders).  All outliers were removed, this included cars with a price less than $500 which was not realistic.  After all this was done, the Data Understanding process was revisited by replotting all the previous graphs to see if the cleaning process created more coherent data.

MODELING:

Based on the hypothesized linear nature of the relationship between the data features and the price of cars, several linear models were selected and used to train several candidate models.  LASSO and Ridge linear models were used with Standard Scalers.  GridSearchCV was used to find the best Alpha values for the LASSO and Ridge model.  A polynomial feature Linear Regression model was tested with degrees 1 through 4.  The polynomial feature model used simple cross validation as the cross validation method.   K-Fold Cross validation was used to ensure that the models had the right level of fit for both the LASSO and Ridge models.  RFE was used to select the 5 top features for the Ride and LASSO models.

EVALUATION:

The ridge, polynomial and LASSO variations of the models were tested by calculating the Mean Squared Error of each model.  The number of folds for K-Fold and Alpha values were varied and tested several times to see their effect on what model would be the best one.  
For the best model, permutation Importance was used to find out what features had the highest correlation with price, and which ones could be used to advice a Car sales company on what to focus on in their car sales.  Permutation Importance was used because it clearly ranks the features according to their correlation with the price. From the evaluation it was determined that a polynomial Linear Regression model with a degree of 2 was the best performing model.  Permutation Importance accertained the following features as being the most important when using the polynomial model:

year    0.766 +/- 0.065
odometer 0.456 +/- 0.168
type    0.436 +/- 0.036
fuel    0.300 +/- 0.029
cylinders 0.214 +/- 0.012
transmission 0.075 +/- 0.016
condition 0.060 +/- 0.016
size    0.035 +/- 0.005.

Please see provided Jupiter notebook for the corresponding MSE for each model and their unique features.

DEPLOYMENT:

Based on the steps above, the best model was the polynomial model:   and the most important features were determined to be:  Year, Odometer and type.  This seems to be consistent with what is expected in the real world.  Older cars would tend to have more mileage on the odometer and thus cost less.  The type of car would definately affect the sales price as luxury cars tend to cost more.  The Store owner of the user cars should focus on these three characteristics of the cars he sells.


The recommended next steps would be to test the data again with an external data set to see if the current model is  too fitted to the data.  By performing predictions with another very similar data set that is not part of the current dataset, it can be determined if the model is under or overfitted.  Also further work may need to be done to remove features that are highly correlated:  For example, the year a car was produced may be correlated to its condition and so the model may possibly be simplified to use just one of those features.
