# Recipe_site_traffic
# Table of Contents
[I. Project Statement](https://github.com/nhh979/Bike_Sharing_Demand_proj/tree/main#i-problem-statement)  
[II. Dataset](https://github.com/nhh979/Bike_Sharing_Demand_proj/tree/main#ii-dataset)  
[III. Data Exploring](https://github.com/nhh979/Bike_Sharing_Demand_proj/tree/main#iii-data-pipeline)  
[IV. Data Preprocessing and Model Building](https://github.com/nhh979/Bike_Sharing_Demand_proj/tree/main#iv-eda-summary)  


## I. Project Statement
Tasty Bytes is a search engine platform for food recipes. The task is to analyze the given and write a report with findings to help decide to choose which recipes to display on the homepage each day. 

## II. Dataset
The dataset contains 947 rows and 8 columns.

|Column Name |Details|
|---|---|
|recipe|Numeric, unique identifier of recipe|
|caloris|Numeric, number of calories|
|carbohydrate|Numeric, amount of carbohydrates in grams|
|sugar|Numeric, amount of sugar in grams|
|protein|Numeric, amount of protein in grams|
|category|Character, type of recipe ('Lunch/Snacks', 'Beverages', 'Potato','Vegetable', 'Meat', 'Chicken, 'Pork', 'Dessert', 'Breakfast', 'One Dish Meal')|
|servings|Numeric, number of servings for the recipe|
|high_traffi|Character, if the traffic to the site was high when this recipe was shown, this is marked with “High”.|

## III. Data Exploring
**1. Analyze Data:** Explore some characteristics of the dataset such as its dimension, missing values, duplicated rows, and data type of each variable. 

**2. Exploratory Data Analysis (EDA):** This is a crucial process that gives us a deeper understanding of the dataset. Some insights I got from EDA phase such as 
- All numerical variables have right-skewed distributions
- The Breakfast recipe makes up the highest number of recipes (106 out of 947 recipes, accounting for 11.2%)
- Pork recipe has the largest average amount of calories, Potato recipe has the highest average amount of carbohydrate, Dessert recipe has much much more Sugar than other recipes, and similarly Chicken Breast has the most average amount of protein
- Potato, Vegetable and Pok recipes are popular recipes since they made really high site traffic. Conversely, Beverages recipe is the least popular recipe.

**3. Data Cleaning:** 
- Dropped `recipe` column
- Removed rows that contained missing value in all of four columns `calories`, `carborhydrate`, `sugar`, `protein`
- Made the data in `servings` column consistent
- Converted data in `high_traffic` column into numeric data

## IV. Data Preprocessing and Model Building
**1. Feature Engineering:** I double-checked the `calories` column and found out there were a lot of unresonably low values in the column. I recalculated and replaced those values using the formula `calories = 4 * (carbohydrate + protein + sugar), according to [Food and Nutrition Information Center (FNIC)](https://www.nal.usda.gov/programs/fnic). I then dummy variables for each categorical columns.

**2. Evaluation Metric:** The task requirement is to predict the recipes correctly 80% of the time and simultaneously minimize the chance of showing unpopular recipes. I thus decided to use `Accuracy Score` as the main metric.

**3. Model Training:** I tried multiple models such as Logistic Regression, K-Nearest Neighbor, Decision Tree, Random  Forestand, XGBoost and Support Vector Machine. I then did hyperparameter tuning using GridSearchCV and RandomizedSearchCV to find the best estimator. 

**4. Model Evaluating:** Comparing the accuracy scores between those models I figured out **Logistic Regression, K Nearest Neighbors,** and **Support Vector Machine** had better performance because they provided high accuracy and less overfitting than other models based on **Accuracy score using 10-Fold Cross-Validation**. Out of those three model, **Support Vector Machine** model's performance is the best with the accuracy score of 80.2%.


