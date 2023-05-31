# CryptoClustering
An unsupervised learning project and general ML process exploration using crypto market data.

## Procedure

### Prepare the Data
1. Use the `StandardScaler()` module from `scikit-learn` to normalize the data from the CSV file.

2. Create a DataFrame with the scaled data and set the 'coin_id' index from the original DataFrame as the index for the new DataFrame.

3. The first five rows of the scaled DataFrame appear as follows:
    ![Scaled DataFrame head](/images/scaled_df.png)

### Find the Best Value for $k$ Using the Original Scaled DataFrame
Use the elbow method to find the best value for $k$:
- Create a list with the number of $k$ values from 1 to 11.
- Create an empty list to store the inertia values.
- Create a for loop to compute the inertia with each possible value of $k$.
- Create a dictionary with the data to plot the elbow curve.
- Plot a line chart with all the inertia values computed with the different values of $k$ to visually identify the optimal value for $k$.
    
    ![Original elbow curve](/images/orig_elbow.png)

### Cluster Cryptocurrencies with $k$-means Using the Original Scaled Data
Use the following steps to cluster the cryptocurrencies for the best value for $k$ on the original scaled data:
- Initialize the $k$-means model with the best value for $k$.
- Fit the $k$-means model using the original scaled DataFrame.
- Predict the clusters to group the cryptocurrencies using the original scaled DataFrame.
- Create a copy of the original data and add a new column with the predicted clusters.
- Create a scatter plot using hvPlot:
    - Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d".
    - Color the graph points with the labels found using $k$-means.
       - Add the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.
       
    ![Original clustering](/images/orig_clusters.png)

### Optimize Clusters with Principal Component Analysis
Using the original scaled DataFrame, perform a PCA and reduce the features to three principal components.

Retrieve the explained variance to determine how much information can be attributed to each principal component and then answer the following question in your notebook:

What is the total explained variance of the three principal components?
Create a new DataFrame with the PCA data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.

The first five rows of the PCA DataFrame should appear as follows:

The first five rows of the PCA DataFrame

### Find the Best Value for k Using the PCA Data
Use the elbow method on the PCA data to find the best value for k using the following steps:

Create a list with the number of k-values from 1 to 11.
Create an empty list to store the inertia values.
Create a for loop to compute the inertia with each possible value of k.
Create a dictionary with the data to plot the Elbow curve.
Plot a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k.

Answer the following question in your notebook:
What is the best value for k when using the PCA data?
Does it differ from the best k value found using the original data?

### Cluster Cryptocurrencies with K-means Using the PCA Data
Use the following steps to cluster the cryptocurrencies for the best value for k on the PCA data:

Initialize the K-means model with the best value for k.
Fit the K-means model using the PCA data.
Predict the clusters to group the cryptocurrencies using the PCA data.
Create a copy of the DataFrame with the PCA data and add a new column to store the predicted clusters.

Create a scatter plot using hvPlot:
- Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d".
Color the graph points with the labels found using K-means.
Add the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point.

### Visualize and Compare the Results

![Elbow compare](/images/elbows.png)
![Cluster compare](/images/clusters.png)

While the scatterplot representation of the clusters appears to have changed drastically, it seems that we have approximately the same distribution of data points within each cluster, with similar separation as represented in a 2-dimensional plane. This, along with the variance capture measures examined above, indicates that condensing the data through principal component analysis has not resulted in significant information loss.
