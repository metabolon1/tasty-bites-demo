# Summary Report - Predicting Tasty Bites Web Traffic
This is the final project for my professional-level Data Scientist certification exam through DataCamp. It consists of a fictitious business problem. 

## Project Overview and Goals
The home page for Tasty Bites, a fictious company, displays a different recipe every day. The product manager has observed that certain recipes substantially boost traffic to their website. Higher traffic leads to more subscriptions, which is beneficial for the company.

The Product Manager wants us to correctly predict popular recipes 80% of the time. In statistical terms, this equates to building a model with 80% precision. Thus, our KPI is model precision.

I was presented with a dataset of recipe information, including which ones were popular. I determined this to be a classification problem. I used the dataset to develop models, and used 80% precision as the threshold for evaluating model performance.

## Key Findings
- Two different models (decision tree and logistic regression) were evaluated head-to-head, primarily on the basis of their ability to reliably meet the 80% precision target.
- Winning model: a one-node decision tree, which was able to reliably predict popular recipes at least 80% of the time by selecting only recipes from certain categories.
- This model is easy to understand, implement, and and tweak as needed by the Product team.
- I recommend displaying recipes from each of the five aforementioned categories in approximately equal proportions, perhaps on a rotation.
- Performance should be monitored using both 30- and 90-day moving averages of precision.

## Validation and Exploratory Data Analysis (EDA)
The sample dataset consisted of 947 recipes and 8 variables:
- `recipe`: a unique identifier
- `high_traffic`: indicates whether recipe generated high website traffic (i.e., was popular)
- `calories`/`carbohydrate`/`sugar`/`protein`: nutritional information about each recipe
- `servings`: number of servings
- `category`: e.g., Beverage, Pork, Dessert

I performed the following validation tasks:
- verified that `recipe` identifiers were unique, with no missing values.
- discovered that using the values in `calories`, `carbohydrate`, `sugar`, and `protein` derive non-sugar carbohydrates (g) and fat (g) content yielded negative values, which is physically possible. Thus, I determined these variables to be invalid and did not use them for model development.
- cleaned up the `category` variable, consolidating two chicken categories into one and converting to a factor.
- cleaned up the `servings` variable and converted to numeric.
- converted `high_traffic`, the target variable, into a logical for ease of calculation.

After validation, only two candidate predictors remained: `category` appeared to be highly informative with respect to recipe popularity, while `servings` did not.

![](/Images/recipe_counts_by_category_colored_traffic.png | width=100)

## Model Training and Evaluation

I used an 80/20 split to generate a training and testing dataset. I trained two models for predicting recipe popularity:
- Baseline model: a simple, 1-node decision tree based on inclusion or exclusion in a subset of recipe `category`.
- Comparison model: a logistic regression based on both `category` and number of `servings`. `servings` was again shown to be uninformative.

The criterion I used for model evaluation was whether the lower bound of the one-sided 95% Wilson confidence interval of precision was greater than or equal to 80% for the test dataset. I chose this criterion to ensure a 95% chance of meeting the KPI target. While both models had similar confidence intervals for precison, only the baseline model strictly met the KPI criterion.


This failure of the comparison model is attributed to a low classification threshold rather than to the inclusion of the servings variable. Had I set the classification threshold a little higher, I suspect that the comparison model would have also met the KPI target. `servings` had a negligible affect on model characteristics, introducing a small amount of noise but otherwise not affecting predicitve ability much.

As would be expected, the model with slightly lower precision (i.e., comparison model) had slightly higher recall. In other words, because it was less picky, it was able to identify more of the popular recipes at the expense of also misidentifying more unpopular recipes as popular.


To improve the odds of displaying popular recipes at least 80% of the time, the product team should employ the 1-node decision tree model, displaying only recipes from the following five categories (ranked by popularity, high to low): Vegetable, Potato, Pork, Meat, and One Dish Meal. To start, the mix across categories should be even (perhaps on a rotation). 

We should monitor the 30- and 90-day moving averages of the proportion of popular recipes displayed. If both moving averages dip below 80%, the product team should consider removing the less popular categories from among the list of five.

If this strategy also fails to meet the KPI, or if more recipe variety is desired, then we will need a greater variety of predictor variables, such as accurate nutritional data, prep time, and cost. This should allow the data science team to better identify popular recipes, especially in the less popular categories, thus meeting desired precision while improving recall.
