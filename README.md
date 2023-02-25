# Calories and Minutes
Project 3 for DSC 8

## Introduction

When beginning this project, we established and faced an ultimate question: what types of cooking recipes have the most calories? By solving this question, one could provide solid concrete evidence for non-nutrition related factors for high calorie count. If these factors exist, there would be more factors that cooks could take into account in order to make the lowest, or highest, calorie counted recipes.

In this project, the provided data was derived from two .csvs of data scraped from food.com: RAW_recipes.csv and RAW_interactions.csv. The resulting data frame was merged using pandas into a single dataframe, keeping only RAW_interactions rows that were in RAW_recipes. After calculating and adding a column to keep track of average ratings for each recipe, the table consisted of 234429 rows and 16 columns. However, the only columns we will be focusing on for this project are the minutes column and the nutrition column, which we will later extract the calories from. The minutes column contains the number of minutes required for each recipe in the dataset, while the nutrition column has the nutrition content in the form of stringed lists, which we will later be extracting the calorie information from.

## Cleaning and EDA

While cleaning the given data, I focused on three main things: removing outliers and unnecessary data, changing data to more useful formats, and accessing needed data. I began the cleaning by dropping the following columns: review, name, recipe_id, contributor_id, submitted, user_id and date, which I believed would not be of interest to us on this project. I also dropped several outlier values. For instance, minute values that were either too big or zero. I set a maximum threshold of three days for the minutes, or 4320 minutes. I then removed all minutes that had value zero, as recipes should take some form of time. In terms of reformatting data, I changed the stringed list columns of nutrition, tags and ingredients to lists, as well as nutrition, which we would be using later on in the project. After this, I turned each nutrition value into its own columns, then dropped the columns that were not the calorie value.

### Univariate Plot
<iframe src="assets/univariate_plot.html" width=800 height=600 frameBorder=0></iframe>
In this plot, we notice that the general distribution of all minute are below 100 minutes, making the majority of recipes less than
100 minutes long.

### Bivariate Plot
<iframe src="assets/bivariate_plot.html" width=800 height=600 frameBorder=0></iframe>
Here the number of calories seem to increase as the recipe decrease in time length. There is also a higher concentration of data in the 
shorter recipes.

### Aggregation

| bool_minutes   |   minutes |   calories |
|:---------------|----------:|-----------:|
| False          |  151.715  |    469.967 |
| True           |   23.8409 |    340.853 |
In this table we decide to sort minute values into ones greater than 50 and ones less than 50, as they seem to hit their peak there.
By aggregating by this new boolean column and calling mean, we get the resulting table.
The table seems to show that shorter recipes have more calories on average.