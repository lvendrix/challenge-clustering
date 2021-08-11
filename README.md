# Challenge Clustering - Defective Bearings

## Mission objectives

Our team was hired to make an automated bearing testing system and was asked to make a model to use in a scheduled maintenance system. A sample of the bearings in use of their new-fangled machine would be tested, and your model would predict whether a bearing is faulty or not.

We'll implement different clustering algorithms to identify possible clusters. This project is mostly based on KMeans while also looking at other clustering algorithms.

# Installation

## Python version
* Python 3.9

## Packages used

* pandas
* numpy
* matplotlib.pyplot
* seaborn
* plotly.express
* operator
* itertools
* sklearn
* yellowbrick

# Usage

| Filename                             | Usage                                                     |
|--------------------------------------|-----------------------------------------------------------|
| bearing_clustering.ipynb | Jupyer Notebook file containing Python code.<br>Used to clean the data.<br>Used to draw plots and do preliminary analysis. <br>Used to find clusters using different clustering algorithms.|
| data_bearings_classification.csv | csv file containing information about bearings|
| Visuals | Folder containing visuals.|

# First steps
* To ease the process of clustering, we have only selected 8 columns (all related to the 'mean') instead of the 53 original ones.

![](/Visuals/Visual_columns.png)
* After selecting those 8 columns, we have also normalized the data (0-1)

# Clustering
Before creating any function to iterate over all the possible combinations of features and see which ones lead to the best silhouette-score, we first plotted all the features in a scatter-matrix to have a first look at their relation and discover possible clusters.

![](/Visuals/Visual_Scatter_Matrix.png)

Based on this scatter-matrix, we started to play around with features that seemed interesting. For example here: 'hz_mean', 'a2_x_mean', 'a2_z_mean' with 3 clusters yield interesting results (score of 0.84).

![](/Visuals/Visual_3_features_original_gif.gif)

Now, we create 3 functions to iterate over all possible combinations:
* combination_features(df, number_features): Takes a dataframe and the desired number of features to be combined. Outputs a list
* score_features(df, list_combinations, max_number_clusters, random_state): Takes a dataframe, a list of combinations, a maximum number of cluster and a random state. Outputs a dictionary of the top-10 combination of features, based on the silhouette score.
* plot_features(df, dictionary): Takes a dataframe and a dictionary. Outputs a 2d scatter-plot if 2 features, a 3d scatter-plot if 3 features, and nothing if more than 3 features. Will also plot a silhouette plot. 

![](/Visuals/Visual_3_features_best_gif.gif)

# Results
Best silhouette scors sfor n features (KMeans++) using all the dataset
| # features | Clusters | Score |  
| ---------- | -------- | ----- |
| 2          | 2        | 0.956 | 
| 3          | 2        | 0.917 |
| 4          | 2        | 0.882 |
| 5          | 2        | 0.846 |
| 6          | 2        | 0.82  |

![](/Visuals/Visual_evolution_score.png)

# Conclusion 
As we can see, the best scores are always with a cluster of size 2, and the silhouette score keeps decreasing as we increase the number of features used to cluster.
It seems that we have 3 possible outliers that create their own cluster. By having values very dissimilar to the rest, it creates a nice separation between clusters. However, they are only 3 bearings in that cluster which is very unbalanced. We could also remove those from the dataset and redo the clustering search with the updated dataset.

# Further investigation
* Try other clustering methods and see if we have a better score
* Investigate possible 'outliers' affecting the performance of KMeans

# Timeline
09/08/2021 - 11/08/2021
