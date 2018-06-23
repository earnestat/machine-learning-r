---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 03-Unsupervised-Learning-II.md in _episodes_rmd/
title: 'Unsupervised Learning II: clustering'
author: "Hugo Bowne-Anderson, Jorge Perez de Acha Chavez"
questions: 
- "What is clustering?"
objectives: 
- "Know the basics of clustering."
- "Perform the k-means algorithm in R."
- "Learn how to read a confusion matrix."
keypoints: 
- "Clustering may reveal hidden patterns or groupings in the data."
- "A confusion matrix is a tool that allows us to measure the performance of an algorithm."
output: html_document
---





## Unsupervised Learning II: clustering

One popular technique in unsupervised learning is _clustering_. Essentially, this is the task of grouping your data points, based on something about them, such as closeness in space. What you're going to do is group the tumour data points into two clusters using an algorithm called k-means, which aims to cluster the data in order to minimize the variances of the clusters.

Cluster your data points using k-means and then we'll compare the results to the actual labels that we know:


~~~
# k-means
km.out <- kmeans(df[,2:10], centers=2, nstart=20)
summary(km.out)
km.out$cluster
~~~
{: .language-r}

Now that you have a cluster for each tumour (clusters 1 and 2), you can see how well they coincide with the labels that you know. To do this you'll use a cool method called cross-tabulation: a cross-tab is a table that allows you to read off how many data points in clusters 1 and 2 were actually benign or malignant respectively.

Let's do it:



~~~
# Cross-tab of clustering & known labels
CrossTable(df$X2, km.out$cluster)
~~~
{: .language-r}

> ## Discussion
>
> How well did the k-means do at clustering the tumour data?
>
{: .discussion}