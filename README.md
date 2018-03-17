[![Build Status](https://travis-ci.org/UBC-MDS/ssgkmeansr.svg?branch=master)](https://travis-ci.org/UBC-MDS/ssgkmeansr)

# ssgkmeansr

An R package for k-means clustering.

## Contributors

Sophia Wang, Susan Fung, Guanchen Zhang

## Description

This is the repository for the R version of the `ssgkmeansr` package. The Python version is available [here](https://github.com/UBC-MDS/ssg_pymeans).

This package implements the classical unsupervised clustering method, [k-means](https://en.wikipedia.org/wiki/K-means_clustering), for two-dimensional datasets with options for choosing the initial centroids (e.g. random and kmeans++). Users will be able to find clusters in their data, label new data, and observe the clustering results.

## Functions

The package implements the following functions:

- initial points selection:
  -  basic k-means: initial centroids are picked randomly.
  -  k-means++: initial centroids are picked based on distance. More details can be found [here](https://en.wikipedia.org/wiki/K-means%2B%2B).
- clustering: build clusters and save cluster attributes
- prediction: predict the label of new data based on the cluster attributes
- plotting: the package will provide plotting functions to visualize the results and performance

Outputs related to performance (within cluster sum of squared distance) is part of the output from clustering.

The package includes two datasets for testing and demonstration.

## Installing the Package

Run the following command in R:

`devtools::install_github("UBC-MDS/ssgkmeansr")`

## Examples
```
# Generate test data frames
set.seed(46)
var <- .15
feature_one <- c(rnorm(5,-1, var),rnorm(5,0, var),rnorm(5,1, var))
feature_two <- c(rnorm(5,-1, var),rnorm(5,0, var),rnorm(5,1, var))

data_train<- data_frame(x1 = feature_one,
                        x2 = feature_two)

set.seed(1)
var <- .1
feature_one <- c(rnorm(5,-1, var),rnorm(5,0, var),rnorm(5,1, var))
feature_two <- c(rnorm(5,-1, var),rnorm(5,0, var),rnorm(5,1, var))

data_test <- data_frame(x1 = feature_one,
                        x2 = feature_two)

# Build clusters
cluster <- fit(data = data_train, K = 3, method = "kmpp")

# predict the label of new data based on the cluster attributes
result <- predict(data = data_test, centroids = cluster[[3]])

# Plot scatterplot for new data with cluster labels
kmplot(dat = result)
```

## Ecosystem

Similar packages:

- [kmeans in the stats package](https://stat.ethz.ch/R-manual/R-devel/library/stats/html/kmeans.html)
- [flexclust](https://cran.r-project.org/web/packages/flexclust/flexclust.pdf)

`ssgkmeansr` is intended to help understand the fundamentals of k-means and variants. Contributors are encouraged to build advanced features on top of this base k-means package.
