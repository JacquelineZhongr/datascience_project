# Recipe Investigation: 
# Part I: What types of recipes tend to have higher average ratings?


## Introduction
<br />
The dataset is merged by two datasets drawn from a real food recipe website Food.com since 2008. One of the datasets record the features of recipes, and another one record the comments by users towards a recipe. We merge the two datasets by recipe id, so each of the row correspond to a recipe's features and a feedback from a user. The question we Investigate in this project is: What types of recipes tend to have higher average ratings?<br />
<br />
This is a real-world dataset about how cooking learners rate the recipe. This question analyze the factors associated with rating, which can help contributors/posters of recipe understand how to write or design the recipe.It has 234429 rows and 18 columns. The relevant columns are: 'id', an unique number assigned to a recipe; 'minutes', time to prepare for the recipe; 'nutrition', a list of number correspond to percentage of daily value of 7 kinds of nutrients; 'n_steps', number of steps in the recipe; 'rating', an integer rated by a user for the recipe.<br />


---

## Cleaning and EDA
### Data cleaning
To explore the question using different analysis tool, data cleaning is needed on the raw data, <br /><br />
•First step: we discard part of features in the dataframe and only preserve columns with features related to the question, namely columns 'name', 'id', "minutes', 'nutrition', 'n_steps', 'n_ingredients' and 'Average_rating'. By doing this, we eliminated irrelevant data which make our data analyzing process more efficient. <br /><br />
•Second step: we prep our data for further analysis by looking at the types of each columns and identifying which column is need to be typecasted. We found that type casting is needed to be applied on column 'nutrition' since they are string representation of a list with nutrition info like calories, sugar etc as elements. We then extrated these elements from 'nutrition' column, split them and make a new column for each nutrition info in our dataframe. For each new column, we typecasted them into 'float' for further analysis. After getting all info out of the 'nutrition' column, we dropped the column to make the dataframe less redundant.<br />
<br />•Third step: by merging two dataframe(information about each recipes and users reviews on the recipes), one recipe can appear in many rows if more than one users leave review for it(each reviews for the same recipe would take one line). Also, to explore the question we have, we just need infomation about the recipe and also average rating. Since we already calculated the average rating and assign to each rows(rows of identical recipe would have the same average rating), we decided to drop duplicates based on the "id" column which stores the unique number for individual recipe. By doing this, we can use count to perform data analysis without being influence by having one recipe appear more than others in the dataframe and eliminate potential bias.<br /><br />
The first five rows of the cleaned dataframe are as below: 
<br />

|    | name                                 |     id |   minutes |   n_steps |   n_ingredients |   rating |   Average_rating |   calories (#) |   total fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated fat (PDV) |   carbohydrates (PDV) |
|---:|:-------------------------------------|-------:|----------:|----------:|----------------:|---------:|-----------------:|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |        10 |               9 |        4 |                4 |          138.4 |                10 |            50 |              3 |               3 |                    19 |                     6 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |        12 |              11 |        5 |                5 |          595.1 |                46 |           211 |             22 |              13 |                    51 |                    26 |
|  2 | 412 broccoli casserole               | 306168 |        40 |         6 |               9 |        5 |                5 |          194.8 |                20 |             6 |             32 |              22 |                    36 |                     3 |
|  6 | millionaire pound cake               | 286009 |       120 |         7 |               7 |        5 |                5 |          878.3 |                63 |           326 |             13 |              20 |                   123 |                    39 |
|  7 | 2000 meatloaf                        | 475785 |        90 |        17 |              13 |        5 |                5 |          267   |                30 |            12 |             12 |              29 |                    48 |   

### Univariate Analysis
In this section, we choose to visualize the distributions of two variables: number of steps and number of ingredients.<br />
<br />
1.Distribution of Steps Number(n_steps)<br />
<br />
According to the diagram, the number of recipes increases in each category as n_steps increases from 1 to 7 and decreases from 7 to 40. Most of the recipes falls in the n_steps range from 1 to 20, and n_steps 7 has the highest count, about 7000. Only very few recipes have n_steps from 40 to 100.
<iframe src="assets/n_steps_distribution.html" width=800 height=600 frameBorder=0></iframe>
<br />
<br />
2.Distribution of Ingredients Number(n_ingredients)<br />
<br />
According to the diagram, the number of recipes in each category increases as n_ingredients increases from 1 to 8 and decreases from 8 to 20. Most of the recipes falls in the n_ingredients range from 1 to 20, and n_ingredients 8 has the highest count, about 9000. Only very few recipes have n_ingredients from 20 to 35.
<iframe src="assets/n_ingredients_distribution.html" width=800 height=600 frameBorder=0></iframe>
<br />

### Bivariate Analysis
In this section, we explore more about the correlation of n_steps / n_ingredients with average rating. Because the average ratings include many different floats and make the diagram hard to observe, we round the average ratings to its nearest integer.<br />
<br />
1.Average Rating vs Step Number<br />
<br />
This is the box plot with average rating on the x-axis and n_steps on the y-axis. We observe that for each category of average ratings(1,2,3,4,5), interquartile range of its corresponding steps are from 6 to 15, meaning that the middle 50% of the data points fall in the range. Also, the minimum to maximum n_steps in range is from 1 to 25 for each of the ratings. Therefore, given a recipe with n_steps from 1 to 25, it is hard to conclude which average rating range it may fall in. <br />
However,there are also many outliers in this plot, especially for the rating of 5 category and most of them are recipe with more steps. The plot suggests that a recipe with n_steps from 40 to 60, it is more likely to fall in the rating 4 or 5. If a recipe has step number over 60, it is very likely fall in the rating 5. Since there are only fewer number of recipes with number over 60 comparing to below 60, these data may not be representative enough to predict the rating.

<iframe src="assets/n_step_box.html" width=800 height=600 frameBorder=0></iframe>
<br />
2.Average Rating vs Ingredient Number<br />
<br />
This is the box plot with average rating on the x-axis and n_ingredients on the y-axis. We observe that for each category of ratings(1,2,3,4,5), interquartile range of its corresponding ingredients are from 6 to 12. Also, the minimum to maximum n_ingredients is from 1 to 20 for each of the ratings. Therefore, given a recipe with n_ingredients from 1 to 20, it is hard to estimate a average rating for it. However,there are also some outliers in this plot.  The plot suggests that a recipe with n_ingredients over 30 only falls in rating of 5. Thus, if given a recipe with n_ingredients over 30, it is more likely to have an average rating of 5.

<iframe src="assets/n_ingredients_box.html" width=800 height=600 frameBorder=0></iframe>
<br />

### Interesting Aggregates
To explore the relationship between number of steps it take to make the food('n_steps') and the average rating, I have grouped and labeled recipe with average rating that fall in range [0,1] (including on both side as [0,1]), recipe with average rating that fall in (1,2] (including 2 but excluding 1) as (1,2] and  same for (2,3], (3,4], (4,5]. <br /><br />
Also for step range, I label each n_step as [0,20], (20,40], [40,60), [60,80), (80,100]. Then we created the pivot table as shown below with average rating range as columns and step range as index for rows. Each values indicate the percentage of data in each step range fall into each average rating range individually. <br /><br />
Each row sum up to 100% and to avoid biases that may be introduced by the missingness, we also drop the nan values in the average rating column, leaving all valid average rating. 
<br />

| step range   |      [0,1] |     (1,2] |    (2,3] |    (3,4] |      [4,5] |
|:-------------|-----------:|----------:|---------:|---------:|-----------:|
| [0,20]       | 0.00692185 | 0.00753534| 0.0331022| 0.169045 | 0.783396   |
| (20,40]      | 0.00787919 | 0.0111622 | 0.0308601| 0.159991 | 0.790107   |
| (40,60]      | 0.00980392 | 0.00490196| 0.0245098| 0.102941 | 0.857843   |
| (60,80]      | 0          | 0         | 0.04     | 0.04     | 0 .92      |
| [80,100      | 0          | 0         | 0.1      | 0.169845 | 0.8        |

<br />
This pivot table give a good representation of the average rating distribution for each step range interval becasue instead of looking at the number of recipe fall in these ranges, we use the percentage which eliminate the potential biases caused by population differences(the total recipes number in certain step range is more than others).<br /><br />
By looking at the table, we observed that recipes with step between 60-80 tend to have higher rating since more than 92 percent of these recipe have average rating between 4 and 5 with 0% percent that fall in average rating between 0-2. Morover, the distribution of average rating for step range (60,80] is different than others, with a tendency to fall in higher average rating. However, this observation is needed to be supported using statistical analysis tools. 

---
## Assessment of Missingness
Since in the data cleaning process, we dropped duplicated rows(rows with identical recipe) to explore the question we have. However, by doing this, we potentially dropped rows with nan values in columns that should not be excluded when accessing the missingness relationship. Therefore, in this section, we would use the cleaned dataframe without dropping the duplicates (dataframe without performing Step Three) to take in account of every nan values for accuracy purposes. <br />

### NMAR Analysis
One column with missingness we found that could be NMAR is the "description" column.<br />
By putting description for recipes for their recipes, the recipe creater can introduce and provide more information about what their dishes is like. One NMAR explantion for missingness existed in "description" column could be that the dishes is too commonly known among people. One example is french fries. Even without description, people would know what french fries is and that recipe they are looking at, therefore, the recipe creater may leave it blank due to the reason that the desctiption if they ought to put is too obvious and may seem useless. <br />
Another case could be the dish is too uncommonly known which required many inforamtion or the description is too complicated if they ought to have one. Therefore, they may leave it blank as the description would be more lengthy and redundant than the recipe itself.<br />
The additional information that is required to explain the missingness could be "popularity“ which indicate the level of familiarity people are with the dishes(from 1 to 5), thereby make the missingness MAR for "description" column if we ought to add this since if our reasoning is correct, most of missing data would be clustered on level 1 or 5.


### Missingness Dependency
In this section, we investigate the missingness of rating provided by the users. We choose to use rating instead of average rating because each element represent for a datum submitted by a user. We set the significance level at 0.05.<br />
<br />
1.Rating Missingness & n_steps <br />
<br />
Null Hypothesis: the distribution of 'n_steps' when 'rating' is missing is the same as the distribution of 'n_steps' when 'rating' is not missing.<br />
Alternative Hypothesis: the distribution of 'n_steps' when 'rating' is missing is the different from the distribution of 'n_steps' when 'rating' is not missing.<br />
<br />
First, we derive the distribution of 'n_step' of whether 'rating' is missing.
x-axis is the number of n_steps and y-axis is the density of data. The blue line (False) plots the the distribution of 'n_step' of whether 'rating' is not missing, and the red line stands for the distribution when it is missing.<br />
<iframe src="assets/rating_miss_steps.html" width=800 height=600 frameBorder=0></iframe>
<br />
According to the diagram, two distributions are quantitative and look like shifted versions of the same basic shape, so we use the difference in group means as test statistic. After permutation, we get the diagram below, showing the empirical distribution of differences in n_steps means when rating is missing or not. The red line is the observed test statistic, which is the observed difference in n_steps means groupby rating missing. <br />
<iframe src="assets/rating_miss_steps_means.html" width=800 height=600 frameBorder=0></iframe>
<br />
The p_value is 0.0 < 0.05, so it is statistically significant. Thus, null hypothesis is rejected. So it is  likely that missingness of rating is dependent on n_steps, which means that rating is NMAR on n_steps.
<br />
<br />
2.Rating Missingness & minutes <br />
<br />
Null Hypothesis: the distribution of 'minutes' when 'rating' is missing is the same as the distribution of 'minutes' when 'rating' is not missing.<br />
Alternative Hypothesis: the distribution of 'minutes' when 'rating' is missing is the different from the distribution of 'minutes' when 'rating' is not missing.<br />
<br />
First, we derive the distribution of 'minutes' of whether 'rating' is missing. x-axis is the number of minutes and y-axis is the density of data. The blue line (False) plots the the distribution of 'minutes' of whether 'rating' is not missing, and the red line stands for the distribution when it is missing.<br />
<iframe src="assets/rating_miss_min.html" width=800 height=600 frameBorder=0></iframe>
<br />
According to the diagram, two distributions are quantitative and seem to be overlapped with each other. We use the difference in group means as test statistic. After permutation, we get the diagram below, showing the empirical distribution of differences in minutes means when rating is missing or not. The red line is the observed test statistic, which is the observed difference in n_steps means groupby rating missing. <br />
<iframe src="assets/rating_miss_min_means.html" width=800 height=600 frameBorder=0></iframe>
<br />
The p_value is 0.114 > 0.05, so it is not statistically significant. Thus, we fail to reject the null hypothesis. So it is likely that missingness of rating is not dependent on minutes.
<br />
---

## Hypothesis Testing
What we have explored in the pivot table suggests that recipes with step between 60-80 tended to have higher rating, in this section, we would perform hypothesis test to test if this observation is small probability event.<br />
Null hypothesis: the distribution of average rating(range [0-1], (1-2], (2-3], (3-4], (4-5]) for receipes with steps between 60-80 is sampled from the population
<br />
Alternative hypothesis: the distribution of average rating(range [0-1], (1-2], (2-3], (3-4], (4-5]) for receipes with steps between 60-80 is not sampled from the population
<br />
We first calculated the distribution of average ratings for the population and also for the sample(recipe with step between 60-80), perfomed TVD as our test statistic to get the difference between distribution of the two, and then conducted 10,000 trials, generating based on the disctibution for the population to see if the observed distribution difference in the pivot table for recipes with step between 60-80 is due to random chance. 
<br />
The significant level we picked for our test is 0.01 to make our result more robust
<br />
<iframe src="assets/hypothesis_testing.html" width=800 height=600 frameBorder=0></iframe> <br />
<br />
<br />
The p-value we got is 0.0 which imply that we are rejecting the null hypothesis, meaning that there is not enough statistical evidence to infer that the null hypothesis is true. Therefore, the hypothesis test suggest that the distirbution of average rating for recipes with steps between 60-80 is not sampled from the population. This imply that the observation we have in the pivot table may not be result due to random chance and recipes with steps between 60-80 is likely to have different distribution. Combining all observation and test result, we conclude that recipes with steps between 60-80 is more likely to have higher avaerage ratings. <br />


---
# PartII: Predict if the recipe would be labled as "dietary" or not.


## Framing the Problem
### Our Prediction Problem
In today's health-conscious world, there is a growing demand for dietary recipes that cater to specific dietary needs and preferences. Therefore, this model is built helping to predict whether or not one recipe would be tagged with the label "dietary" in food.com given features "ingredients"(ingredients used in the recipe), "minutes"(minutes to prepare recipe), "description"(user-provided description to the recipe), "protein (PDV)", "carbohydrates (PDV)" and "calories (#)".
<br />
### Why this Response Variable?
Our response variable would be "if dietary", either "would be tagged as dietary" or "would not be tagged as dietary" which can be extracted from their tags from the existing dataset for modeling. The reason why we picked this variable is because people are now focusing more and more on their health, and our model aimed to better help the website label their dietary recipes for users who are on diets. These are features that would be available upon time of prediction since the labeling happened after we gain all the information about the recipe, once the user successfully and fully put in all required elements to build the recipe. Moreover, dietary labeled recipes can also have many unique characteristics in menu descriptions, ingredients used, and also nutrition facts.
<br />
### Why F1 as metrics?
Since the prediction only involves yes and no questions, it would be a binary classification problem. We did not choose accuracy because there is a class imbalance between the "would be tagged as dietary" or "would not be tagged as dietary" two classe. The matrices we are using to evaluate our model are F1 since we would take account of the TP(True positive), TN(True negative), FP(False positive),FN(False negative) of the model. When we predict whether it is dietary, we don't give a preference to minimize the FP or FN. Instead, we want to achieve a balance in precision and recall. Thus, F1 distinguishes out of precision or recall.
<br />
## Baseline Model
### About Our Model
We create a tree decision model for our baseline model. Before training the data, we split our dataset into 75% and 25% as training and testing datasets. The hyperparameter we picked are max_depth = 6, criterion = "gini",min_samples_split = 100 since there are 6 features, and "gini" work well with imbalanced data.
<br />
The features we took into our model are "ingredients", "minutes", "description", "protein (PDV)", "carbohydrates (PDV)","calories (#)" which would all be available if at the time of prediction. Among those features, we have 2 categorical and 4 numerical, ingredients(list with ingredients as elm), "description"(a string describing the recipe) are nominal features, and the rest("minutes", "protein(PDV)","carbohydrates (PDV)","calories (#)" are quantitative features. The reasons why we choose "minutes" is because we think dietary meal takes less time to complete since no deep frying is need. Also, a dietary meal tends to have higher "protein(PDV)" and lower "carbohydrates (PDV)" and "calories (#)", but also the balance between those nutrients factors is also what we expect a dietary recipe to have.
<br />
### How Do We Encode Categorical Data?
Before building our baseline model, we first conducted feature engineering on the two nominal features("description" and "ingredients"). 
<br />
For "description", we found that words like "healthy", "low-calorie","gluten-free" and "organic" are likely to be in dietary recipes, therefore we wrote our own FunctionTransformer to transform the "description" feature into True for "having one of these words in the description" and False for "do not have any of them in the description". *True and false can be evaluated as 1 and 0
<br />
For "ingredients", we found that dietary recipes are not likely to have "chocolate" or "bacon" as ingredients. Therefore, we then wrote our own FunctionTransformer to transform the "ingredients" feature into the total occurrence of these two words appearing in the recipes. We use a pipeline to transform and also one-hot encode it.
<br />

### F1 score and Comments
We run the F1 score several times on the trained dataset, and the F1 remains at about 0.71958. Also, the tested data shows a constant accuracy rate of about 0.71538. However, when we calculate the proportion of recipes that have dietary as lable, the proportion is 69%. That is, if the model predicts all the outcome is 5, it can have an accuracy score of 0.69. Our model has a similar F1 score for the testing set(1% higher) and also 1% higher than the model which always predicts as "would be labeled as "dietary" for the testing set which is not very optimal.
<br />

## Final Model
### What Features Did We Add
Built upon the baseline mode, the two features we addd are based on "minutes","protein (PDV)", "carbohydrates (PDV)" and "calories (#)".
After EDA, we found that recipes with label "dietary" are less time-consuming and are more likely to be under 30minutes and minutes has a wide range with extremely large max. Therefore, we perform a Binarizer transformation on "minutes" with threshold 30. By doing this, we divided the recipes in two groups, "with minutes under 30 minutes" and "with minutes above 30 minutes". By doing this, we reduce the dementional of "minutes" and eliminate the extremely large outlier's impact on our model. Then, we also perform QuantileTransformer on the columns "protein (PDV)", "carbohydrates (PDV)" and "calories (#)". Since they are all columns related to the nurtrients and have different scalers, so it is not reasonable to leave them as the raw data. Through QuantileTransformer, we can handle the skewed data, as well as taking care of the effect of outliers, while still perserving the relative relationship. 
<br />

### Model Basics and Grid Search
To compare with the baseline model, we use the same train and test dataset used in baseline model. We still use decision tree because it is still a good choice in classification prediction. To decide the hyperparameters, we perform a GridSearch before training the data. We choose 10 different max_depths, 2 kinds of criterion, and 7 min_samples_split numbers. After training the 140 kinds of combinatio, it comes to the best combination: {'criterion': 'gini', 'max_depth': 7, 'min_samples_split': 50}, and we unpack this combination into our final model.
<br />
### F1 score and Comments
The F1 score in final model for training dataset is 0.72546 and for test dataset is 0.72158. For both of training and testing dataset, the F1 score increases by 1%. An increase by 1% represents the increase in both precision and recall. Also, we attached a confusion matrix below about the distribution of TP, TN, FN, and FP.
<br />
![Screenshot](107851686871529_.pic.jpg)

According to the diagram, the section with the largest number is TP with about 50% dataset there. For the FN and FP part, FP is about 5 times higher than the FN number. This is likely to raise from the bias in dataset itself since the proportion of recipes with "dietary" in tag is higher than recipes without. So as the false prediction, FP is much higher than FN.

## Fairness Analysis
### Hypothesis
In this section, we want to evaluate whether this model is fair. The one variable that relates to whether "dietary" or not is calories number. We want to explore whether this model can gives the same F1 score for calories in different levels. For this question, we will categorize calories to "high_cal", which is higher than and equal to the median calories number in the dataset, and "low_cal" which is lower than the median. We use median as threshold is to have the similiar number of data for those two categories. Then, we explore the data and find that the F1 score of high calories is 4.97% lower than that of low calorie ones. Thus, this leads to:
<br />
Null Hypothesis: Our model is fair. Its F1 score for predicting dietary recipe with high calories and low calories are roughly the same, and any differences are due to random chance. 
Alternative Hypothesis: Our model is unfair. Its F1 score for high calorie recipes is lower than its for the ones with low calories.
Our test statistic is the unsigned difference in low calories and high calories, and signifiance level is p value of 0.05.
<br />
### Conclusion
According to the distribution diagram, the differences normally distribute from -0.04 (-4%) to 0.04(4%), and our observed difference is beyond that range (indicated by the red line).
<iframe src="test.html" width=800 height=600 frameBorder=0></iframe>
<br />
The p_value is 0.0 which is smaller than 0.05 and stastically significant. It rejects the null hypothesis that our model is fair. So it is likely that our model is unfair and tends to predict whether the recipe is dietary when the calorie number is low.






