# Summary Report - Predicting Tasty Bites Web Traffic
This is the final project for my professional-level Data Scientist certification exam through DataCamp. It consists of a fictitious business problem. 

## Project Overview and Goals
- Background: The home page for Tasty Bites, a fictious company, displays a different recipe every day.
- Observation: The product manager has observed that certain recipes substantially boost traffic to their website.
- Implication: Higher traffic leads to more subscriptions, which is beneficial for the company.
- Goal: The Product Manager wants us to correctly predict popular recipes 80% of the time. In statistical terms, this equates to building a model with 80% precision.
- KPI: Precision

## Key Findings
- Two different models (decision tree and logistic regression) were evaluated head-to-head, primarily on the basis of the 80% precision target.
- Winning model: a one-node decision tree, which was able to reliably predict popular recipes at least 80% of the time by selecting only recipes from the following categories:
 - Vegetable
 - Potato
 - Pork
 - Meat
 - One Dish Meal
- This model is easy to understand, implement, and and tweak as needed by the Product team.
- I recommend displaying recipes from each of the five aforementioned categories in approximately equal proportions, perhaps on a rotation.
- Performance should be monitored using both 30- and 90-day moving averages of precision.

## Dataset
