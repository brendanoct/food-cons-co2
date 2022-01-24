# Food Consumption and CO2 Emissions

## Files

Food Consumption and CO2 Emissions.Rmd: .Rmd file which contains the code I used to create this project.

Food-Consumption-and-CO2-Emissions.pdf: Output from RMarkdown in containig full report along with my code.

food_consumption.csv: Original dataset.

images: Contains images to include in README.md.

## Introduction

Carbon Dioxide, or more commonly referred to as CO2, is a greenhouse gas resulting from a number of human activities. When overproduced, it contributes to what is known as the greenhouse gas effect - a natural process that warms the Earth’s surface. What generally happens is when the sun radiates heat and energy, it is either reflected back into space, or it penetrates the earth’s atmosphere, trapped by greenhouse gas to help keep Earth warm enough to sustain life. However, due to the overproduction of greenhouse gases like CO2, this contributes to the levels of greenhouse gas, trapping unnecessary heat within our atmosphere.

This is the underlying cause of what is known as climate change, and is resulting in detrimental effects to the Earth’s climate. One contributor to climate change is the effect of food production. According to a report from [Ritchie and Roser (2020)](https://ourworldindata.org/environmental-impacts-of-food), one-quarter of the world’s greenhouse gas emissions come from the production of food. This suggests that turning our attention on both food and food consumption is integral to targeting the underlying issue of climate change.

## Data

nu3, a German company focusing on supplying supplements and nutritional food products to European countries, have released a [dataset](https://www.nu3.de/blogs/nutrition/food-carbon-footprint-index-2018) exploring food consumption for different food categories, along with their corresponding CO2 emissions, for 130 different countries in 2018. As a result, by utilising the data available, we would like to explore the following questions:

*1. Which countries should we focus on because of their CO2 emissions, both as a whole, as well as for different food categories?*  
*2. Does non-animal product consumption minimise the effects of CO2 emissions from food consumption?*

Fortunately, this data was scraped and cleaned by [Kasia Kulma](https://r-tastic.co.uk/post/from-messy-to-tidy/), so no further cleaning was required.

## Methodology: K-Means Clustering

Through the use of K-Means clustering, we are aiming to group our countries and food categories together so that we can effectively answer the questions we have posed.

K-Means clustering is an unsupervised machine learning technique that aims to partition a datasets observations into K different clusters thorough multiple iterations, in such a way that each observation belongs to only a single group that has similar qualities. Clustering in general takes on an important concept of distance. Distance, in a literal sense, measures how far one thing is from another, however in the world of machine learning, it refers to how similar (or dissimilar) two observations are. The larger the distance between two observations, the less similar they are, and vice versa.

By calculating the Euclidian distance between objects based on defined variables, K-means looks to minimise the “within sum of squares”, while also maximising the “between sum of squares”. In other words, we are looking to cluster our observations in such a way where are minimising the within-cluster dispersion, and maximise the between-cluster dispersion, ensuring that we have clear segments.

Applying K-Means clustering to our data will give us the ability to group our countries that have similar levels of consumption per food group, as well as CO2 emissions, so we can see firstly which countries we should turn our attention to, as well as what food categories in countries we should focus on.

## Evaluating Model

After running our K-Means clustering with a number of different clusters using a for loop, we are able to visibly see which number of clusters is optimal, where optimal is a balance between minimising the “within sum of squares”, while also maximising the “between sum of squares”.

<p float="left">
  <img src="/images/cluster_evaluation_1.png" width="400" />
  <img src="/images/cluster_evaluation_2.png" width="400" />
</p>

As a general rule of thumb, we can choose the number of clusters where the gradient begins to flatten looking at both plots, which is when we choose 4 clusters. This was the case for both of our K-Means clustering, which will be detailed below.

Furthermore, after assessing both of our K-Means clustering, our *between sum of squares to total sum of squares ratio was both above 0.8, or 80%*. This value tells us how good the clustering that our K-Means has found, giving us a measure of the total variance in our data set that is explained by our clustering, indicating that we have split our data fairly accurately.

The two K-Means clustering we performed was for the purpose of answering our first question:

*Which countries should we focus on because of their CO2 emissions, both as a whole, as well as for different food categories?*

# Analysis for countries as a whole

Creating our first K-Means clusters allows us to see very clearly the countries that emit the highest amount of CO2. This was achieved by adding up each of the listed CO2 emissions for each country, and creating our clusters based on consumption and emission. It is clear that those countries in cluster 3 are ones that we should focus on, since they are producing a large amount of CO2 emissions – with their average being 1560.16kg/person/year.

<img src="/images/cluster_graph_1.png" width="500">

# Analysis for countries and specific food categories

However, we want to make use of the data we have and look at countries and their individual food categories. Again, running our K-Means clustering based on both total consumption and CO2 emissions per country and food categories, we are able to see what food categories in each country are responsible for high levels of CO2 emissions.

<img src="/images/cluster_graph_2.png" width="500">

It is evident from our plots for each food category that countries and food categories, cluster 4 are responsible for a high number of CO2 emissions. The food category that is primarily included in this cluster is Beef, but we can also see some Lamb & Goat, from very large number of countries, similar to above. It was found that in this cluster, for each country and food category combination,
there was an average of approximately *20kg/person/year consumed, resulting in almost 640kg/person/year of CO2 emissions*, while all other clusters exhibited a considerably smaller proportion (cluster 1 was the next largest, showing only a 3 times difference between the particular food category consumption and CO2 emissions).

# Analysis of non-animal product consumption

To answer our second research question, it was important to firstly look at the countries that consumed the highest number of non-animal products. In order to account for different levels of consumption between countries, looking at the *proportion of non-animal consumption compared to total consumption* was determined to be a more meaningful measure. By plotting 100 of our 130 countries below, we are able to see the relationship between the proportion of their non-animal consumption compared to total consumption, and their overall ranking in terms of total CO2 emissions from food consumption shows a positive relationship between the two. Labels were also added to countries who had a proportion of non-animal consumption compared to total consumption greater than 0.5. To strengthen this, we have also calculated Pearson’s correlation coefficient between the two variables, attaining a value of 0.71, indicating a moderately strong positive relationship.

<img src="/images/graph_3.png" width="500">

# Conclusion

After performing our analysis, we were able to gain a clear idea of what countries and food categories were responsible for a considerable amount of CO2 emissions. While we were able to gain a list of countries that exhibited high levels of CO2 emissions, what was more insightful to focus on was the different food categories. Beef, lamb and goat were the food categories that were responsible for high levels of CO2 emissions in a number of countries.

Moreover, there is a clear relationship between the proportion of non-animal consumption compared to total food consumption, along with CO2 emissions. Our analysis strongly suggests that countries who consume more non-animal products tend to emit lower amounts of CO2 relative to other countries.

With this analysis we hope that countries can understand the importance of their food choices, and ideally encourage people to consider what they regularly to consume in hopes of slowing down climate change. This could be achieved through a number of different ways, including *decreasing the price of non-animal products, raising awareness on the benefits of consuming non-animal products for both the individual as well as the climate, and also improving accessibility of these products.*
