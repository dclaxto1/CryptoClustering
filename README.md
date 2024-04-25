# CryptoClustering    

- [Introduction](#introduction)
- [Preparing the Data](#preparing-the-data)
  - [Get the summary statistics and plot the data](#get-the-summary-statistics-and-plot-the-data)
  - [Prepare the Data](#prepare-the-data) 
  - [Create a DataFrame with the scaled data](#create-a-dataframe-with-the-scaled-data)
- [Find the Best Value for k Using the Original Scaled DataFrame](#find-the-best-value-for-k-using-the-original-scaled-dataframe)
- [Cluster Cryptocurrencies with K means Using the Original Scaled Data](#cluster-cryptocurrencies-with-k-means-using-the-original-scaled-data)
- [Optimize Clusters with Principal Component Analysis](#optimize-clusters-with-principal-component-analysis)
- [Find the Best Value for k Using the PCA Data](#find-the-best-value-for-k-using-the-pca-data)
- [Cluster Cryptocurrencies with K-means Using PCA Data](#cluster-cryptocurrencies-with-k-means)


## Introduction
Use your knowledge of Python and unsupervised learning to predict if cryptocurrencies are affected by 24-hour or 7-day price changes. 

## Preparing the data

![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/eb7333a5-92e6-49fc-9f98-1a22162ae388)

### Get the summary statistics and plot the data to see what the data looks like before proceeding.

![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/03da8666-f92d-4741-b64e-bd2c0c467aac)

### Prepare the Data Use the StandardScaler() module from scikit-learn to normalize the data from the CSV file.

![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/cc87c70a-2453-4da5-9dd1-b6f9149849a1)

### Create a DataFrame with the scaled data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.

![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/00956870-4334-441a-b382-76cefb029b38)


## Find the Best Value for k Using the Original Scaled DataFrame

Create a list with the number of k values from 1 to 11.  <br />
Create an empty list to store the inertia values. <br />
Create a for loop to compute the inertia with each possible value of k. <br />
Create a dictionary with the data to plot the elbow curve. <br />
Plot a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k. <br />
Answer the following question in your notebook: What is the best value for k? **k=4** <br />

![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/448cbb4e-76bd-4ba8-8bec-d2d2e84ef032)



## Cluster Cryptocurrencies with K means Using the Original Scaled Data

Initialize the K-means model with the best value for k. <br />
*model = KMeans(n_clusters=4, random_state=1)*<br />

Fit the K-means model using the original scaled DataFrame. <br />
*model.fit(crypto_transformed)*

Predict the clusters to group the cryptocurrencies using the original scaled DataFrame. <br />
*k_4 = model.predict(crypto_transformed)*

Create a copy of the original data and add a new column with the predicted clusters. <br />
Create a scatter plot using hvPlot as follows: Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d". <br />
Color the graph points with the labels found using K-means. <br />
Add the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point. <br />
![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/38f5371d-cf7e-4bf4-9cff-8596039033d7)


## Optimize Clusters with Principal Component Analysis

What is the total explained variance of the three principal components? **0.37005408 + 0.32322221 + 0.19115222 = 0.8844285111826466**<br />
Create a new DataFrame with the PCA data and set the "coin_id" index from the original DataFrame as the index for the new DataFrame.<br />
![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/534a36a7-710d-4be4-acc1-2691e02652c0)

## Find the Best Value for k Using the PCA Data 

Create a list with the number of k-values from 1 to 11. <br />
*k = list(range(1,12))*

Create an empty list to store the inertia values. <br />
*inertia2 = []*

Create a for loop to compute the inertia with each possible value of k. <br />
*for i in k:<br />
    k_model = KMeans(n_clusters=i, random_state=1)<br />
    k_model.fit(cluster_pca_df)<br />
    inertia2.append(k_model.inertia_)*<br />
    
Create a dictionary with the data to plot the Elbow curve. <br />
*elbow_data2 = {"k": k, "inertia": inertia2}*

Plot a line chart with all the inertia values computed with the different values of k to visually identify the optimal value for k. <br />
![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/46d475df-0786-4c77-8b8c-8b618a5d1535)

Answer the following question in your notebook: What is the best value for k when using the PCA data?<br />
**I found the best k-value is k=4 when using PCA data**
Does it differ from the best k value found using the original data? <br />
**No, I found it is the same k value as found using the original data**

## Cluster Cryptocurrencies with K-means

Initialize the K-means model with the best value for k. <br />
*model = KMeans(n_clusters=4, random_state=1)*

Fit the K-means model using the PCA data. <br />
*model.fit(cluster_pca_df)*

Predict the clusters to group the cryptocurrencies using the PCA data. <br />
*k_4 = model.predict(cluster_pca_df)(

Create a copy of the DataFrame with the PCA data and add a new column to store the predicted clusters.. <br />
*copy_cluster_pca_df= cluster_pca_df.copy()*

Create a scatter plot using hvPlot as follows: Set the x-axis as "price_change_percentage_24h" and the y-axis as "price_change_percentage_7d". <br />
Color the graph points with the labels found using K-means. <br />
Add the "coin_id" column in the hover_cols parameter to identify the cryptocurrency represented by each data point. <br />
![image](https://github.com/dclaxto1/CryptoClustering/assets/128431134/22c8ffe3-929e-4ced-9bf8-77fd249d338a)


Answer the following question: What is the impact of using fewer features to cluster the data using K-Means?<br />
**Using PCA data resulted in tighter clusters, and it also resulted in more entries within cluster 0 and cluster 1 than the original analysis did.**
