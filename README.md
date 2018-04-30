# Project Proposal: How to Find Healthy Recipes

## 1. Introduction

Eating healthier is a big problem today in the US -- a country which accounts 5% of the world population, but 13% of global overweight and obese people. The American diet is said to be increasingly energy-rich but nutrient-poor (https://academic.oup.com/ajcn/article/82/4/721/4607427). Under this circumstance, there is a belief that cooking from fresh ingredients at home is a much healthier way of eating (https://www.coursera.org/learn/childnutrition), especially compare with eating fast food or processed food. Therefore, cooking healthier would be a great demand of more and more people who want to live a healthier life.

However, how to cook a healthy meal? Where can we find a healthy recipe to cook from the ingredients we have in our refrigerators? How we know it is a healthy recipe and how healthy it is? The first thing I could think to answer these questions is to search on a recipe recommendation website. But after a simple survey of those popular recipe websites, I found that they may not able to fully solve these problems.

Most recipe recommendation websites collect recipes as many as possible from different resources: magazines, cooking books, TV shows, etc., and provide a search engine so that the user could search the recipes they need based on some key words like ingredients, cooking methods or special holiday meals. In most of these websites, some recipes have a tag of "Healthy", but only a tag may not be enough for our problems. One of the most popular recipe websites - allrecipes.com - provides the "healthy" tag but cannot search on the tag. Another website - epicurious.com - is doing a better job by providing searching in a "healthy recipe" subset and giving nutrition facts of most recipes, but it is still hard to know why a recipe is healthy or not, or how healthy a recipe is.

To answer these questions, the first part of this project aims to find out the key features that a healthy recipe should have. In another word, what is the "eigenvector" of healthy recipes? Based on this analysis, we will be able to give each recipe a healthy score, which can guide the user in choosing from different recipes. Furthermore, when we need to build a new recipe, this "eigenvector" could suggest that how to build a healthier one. Then in the second part of the project, I want to provide a search engine that can search like a normal recipe website but also re-rank the search results and recommend healthier recipes.

The dataset I use in the project is from epicurious.com, which is provided by Hugo Darwood on kaggle.com (https://www.kaggle.com/hugodarwood/epirecipes). As I mentioned above, epicurious.com provides "healthy" tag and nutrition facts, which are contained by this dataset and will benefit my project. But if needed, it is also possible to pull more data from other recipe APIs and websites.

## 2. Score a Recipe on Health

Basically, there are two methods to score a recipe on health. The first one is hard coding based on the nutrition facts of a recipe. As Drewnowski (2005) provided in his paper, there are several different indices that can be used evaluate nutrient density (the ratio of the nutrient composition of a food to the nutrient requirements of the human) of a recipe. For example, I used the ratio of recommended to restricted (RRR) food score to build my prototype of healthy recipe search engine (see next section). However, unlike industrial processed food, cooking is a more complex thing and it is hard to say that the nutrition facts table could provide us the information accurate enough. Epicurious.com itself uses a third-party nutrition analysis tool "Edamam Nutrition Wizard" (https://www.edamam.com/website/wizard.jsp), which provides nutrition information according to the ingredients used in a recipe. There are two problems of it: first, we don't know the algorithm or metrics of Edamam; second, cooking methods are not considered.

A more advanced method could be using data mining and machine learning techniques to find out the "eigenvector" of healthy recipes. In the dataset, a typical recipe consists of six parts: title, description, ingredients, direction, categories/tags, and nutrition facts. We can retrieve "healthy" tag from the categories part, which gives us the label we can use in supervised learning. We can apply text mining and other techniques on other parts of recipes, train machine learning algorithms to classify the recipes, and give each recipe a healthy score.

Of cause, we can also combine the two methods to score each recipe. Before deciding the scoring method, I will first do some exploration of the dataset and try to find the distribution of "healthy" recipes (see script on https://github.com/chensong5225/IR_Recipes).

## 3. Search Healthy Recipes

In a search engine of recipes, users typically type in names of ingredients or some special topics (e.g. holiday meals) to search. Since there will be a lot of recipes using the same 1-2 ingredients, we could assume that top n (n could be as large as 100, depends on the size of the dataset) of a normal search result all meet the user's need. If we have a healthy score for each recipe, we will be able to re-rank the normal search result and recommend the healthiest recipes.

With the help from two of my friends, I already build a prototype of the search engine, which will return a list of search result based on the similarity between the query and all the recipe documents, re-rank the list according to RRR score as I mentioned above, and finally give k (k<=n) recipes. The test of the prototype shows that hard coding with RRR scores could have great bias - when we search "chicken", the search engine gives "southern-style fried chicken" at the top of the result, which is far from a healthy meal but might be given a high score because it contains a lot of protein. Choosing another better index or using machine learning method might be able to solve this problem. No matter which scoring method we finally choose, the search engine could be used as a test of the scoring method.

## 4. Conclusion

Healthy lifestyle, including healthy eating and healthy cooking, is one of the most important needs today. Hopefully, the healthy recipe search engine could be developed to a product that can help people achieve a healthier life.