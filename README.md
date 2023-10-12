# Calories and Minutes


## Introduction

When beginning this project, we established and faced an ultimate question: what types of cooking recipes have the most calories? By solving this question, one could provide solid concrete evidence for non-nutrition related factors for high calorie count. If these factors exist, there would be more factors that cooks could take into account in order to make the lowest, or highest, calorie counted recipes.

In this project, the provided data was derived from two .csvs of data scraped from food.com: RAW_recipes.csv and RAW_interactions.csv. The resulting data frame was merged using pandas into a single dataframe, keeping only RAW_interactions rows that were in RAW_recipes. After calculating and adding a column to keep track of average ratings for each recipe, the table consisted of 234429 rows and 16 columns. However, the only columns we will be focusing on for this project are the minutes column and the nutrition column, which we will later extract the calories from. The minutes column contains the number of minutes required for each recipe in the dataset, while the nutrition column has the nutrition content in the form of stringed lists, which we will later be extracting the calorie information from.

## Cleaning and EDA

While cleaning the given data, I focused on three main things: removing outliers and unnecessary data, changing data to more useful formats, and accessing needed data. I began the cleaning by dropping the following columns: review, name, recipe_id, contributor_id, submitted, user_id, tags, steps, ingredients and date, which I believed would not be of interest to us on this project. I also dropped several outlier values. For instance, minute values that were either too big or zero. I set a maximum threshold of three days for the minutes, or 4320 minutes. I then removed all minutes that had value zero, as recipes should take some form of time. In terms of reformatting data, I changed the stringed list columns of nutrition, tags and ingredients to lists, as well as nutrition, which we would be using later on in the project. After this, I turned each nutrition value into its own columns, then dropped the columns that were not the calorie value.

|    |   minutes |   n_steps | description                                                                                                                                                                                                                                                                                                                                                                       |   n_ingredients |   rating |   average_rating |   calories |
|---:|----------:|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|-----------------:|-----------:|
|  0 |        40 |        10 | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              |               9 |        4 |                4 |      138.4 |
|  1 |        45 |        12 | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            |              11 |        5 |                5 |      595.1 |
|  2 |        40 |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 |               9 |        5 |                5 |      194.8 |
|  3 |        40 |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 |               9 |        5 |                5 |      194.8 |
|  4 |        40 |         6 | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 |               9 |        5 |                5 |      194.8 |

### Univariate Plot
<iframe src="assets/univariate_plot.html" width=800 height=600 frameBorder=0></iframe>
In this plot, we notice that the general distribution of all minute are below 100 minutes, making the majority of recipes less than
100 minutes long.

### Bivariate Plot
<iframe src="assets/bivariate_plot.html" width=800 height=600 frameBorder=0></iframe>
Here the number of calories seem to increase as the recipe decrease in time length. There is also a higher concentration of data in the shorter recipes.

### Aggregation

| bool_minutes   |   minutes |   calories |
|:---------------|----------:|-----------:|
| False          |  151.715  |    469.967 |
| True           |   23.8409 |    340.853 |

In this table we decide to sort minute values into ones greater than 50 and ones less than 50, as they seem to hit their peak there. By aggregating by this new boolean column and calling mean, we get the resulting table. The table seems to show that shorter recipes have more calories on average.


## Assessment of Missingness

I could not find a column that was NMAR, as the only columns with missing values were ‘rating’ ‘average_ratings’ and ‘description. It is impossible to tell whether ‘rating’ is NMAR unless I were to fully know the function behind why the ratings were missing. As they came from 0 star ratings, it could be due to other reasons other than default, such as a poorly made recipe or one that simply did not taste good. It is impossible to confirm without this extra information.

### Missingness Plot
<iframe src="assets/missingness_plot.html" width=800 height=600 frameBorder=0></iframe>
As it may be seen in this plot, the distrivution of n_steps when description is missing is very different from when it is not missing.

I believe that the ‘description’ column may be MAR as running a permutation test against the column ‘n_steps’ seemed to result in a resulting p_value of .17, which was above my established alpha value of 0.05. The discrepancy in distributions shown in the plot supports this. Running it against calories resulted in no such correlation, but it is outweighed by the potential correlation with n_steps.

## Hypothesis Testing

For my hypothesis testing, my null hypothesis was thus: "Recipes with more than 50 minutes have more calories on average." Correspondingly, my alternative hypothesis was: "Recipe with more than 50 minutes do not have more calories on average".
I chose these null hypotheses because of two main reasons: the aggregation of the table shown earlier seemed to suggest a trend of higher calories towards lower times, and I chose 50 due to the majority of recipes being below 100 minutes, and having the highest distribution at around 50, which served as a solid middle point. 
The resulting p-value for my permutations was 0.0, which meant that our null hypothesis could not be accepted. By taking a further look at the generated statistics, they seemed to all be much smaller than the absolute mean test statistic. This seems to suggest that the distribution of minutes to calories may not usually be as skewed as on food.com, and would usually be more even.
