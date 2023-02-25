# calories_to_minutes
Project 3 for DSC 8

##Introduction

When beginning this project, we established and faced an ultimate question: what types of cooking recipes have the most calories? By solving this question, one could provide solid concrete evidence for non-nutrition related factors for high calorie count. If these factors exist, there would be more factors that cooks could take into account in order to make the lowest, or highest, calorie counted recipes.
In this project, the provided data was derived from two .csvs of data scraped from food.com: RAW_recipes.csv and RAW_interactions.csv. The resulting data frame was merged using pandas into a single dataframe, keeping only RAW_interactions rows that were in RAW_recipes. After calculating and adding a column to keep track of average ratings for each recipe, the table consisted of 234429 rows and 16 columns. However, the only columns we will be focusing on for this project are the minutes column and the nutrition column, which we will later extract the calories from. The minutes column contains the number of minutes required for each recipe in the dataset, while the nutrition column has the nutrition content in the form of stringed lists, which we will later be extracting the calorie information from.
