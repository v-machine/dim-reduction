# 365Places Dataset Dimensional Reduction 
Dimension reduction methods comparison for large scale image classification.


[Term Project](https://10605.github.io/spring2020/#dimension-reduction-methods-for-image-classification) for [10605 Machine Learning for Large Scale Datasets](https://10605.github.io/spring2020/#dimension-reduction-methods-for-image-classification) </br>
Collaborated with: Jessica Zhu, Amy Lee, Anthony Wu

## Overview
In this project we compare the performance of 3 different dimension reduction techniques which can be deployed in a classification task pipeline. The three methods chosen are PCA, Kernel PCA, and Deep Autoencoder. We use PCA as a baseline to compare again the other two non-linear methods.

## Dataset
We tests our methods on the 365Places dataset, consisting of 1.8 million images (105 GB) of places that are evenly distributed among 365 categories.

## Evaluation:
- Runtime
- Memory Usage
- Reconstruction Error
- Scalability
- Classification Accuracy
- User-friendliness (number of parameters to tune)

## Implementation
The implementation was done using Google Cloud Platform, running Tensorflow on single instances and PySpark on a Dataproc cluster. We had initially implemented PCA and Kernel PCA in spark and autoencoder in tensorflow. But due to Tensorflow lacking native support in Spark, we had decided to move all training to Tensorflow for a consistent comparison. 

## Data Preprocessing
To avoid loading 100GB of data into memory, we rely on batch loading to simultaneously load, preprocess, and store the data on disk. Additionally we decided to reduce image dimensions to 32 by 32 with a single channel to speed up training. 

## Dimensional Reduction
Once the data is preprocessed, we stress-test the three methods to gauge the maximum amount of training data each can handle and obtain a comparison metrics. Based on that we train the best model for each methods.

Using trained model from each method, we performed dimensional reduction to N x 128 on the validation data. We then set up a classification pipeline on a dataproc cluster and train 4 separate logistic regression models: one on the unreduced data (as the controlled group), and 3 on the different dimension-reduced data obtained by the three methods. We then compare their classification performance.

## Result
### Scalability

### Complexity (Runtime)

### Complexity (Memory)

### Reconstruction Error

### Classification Performance

### User-friendliness

### Reconstruction Quality

### Cosine Similarity

## Conclusion
Overall, we concluded that PCA performs the best in terms of computation time, memory usage, and accuracy. However, the Deep Autoencoder appears to be the most scalable, and could be improved if we could determine a way to leverage a distributed system to reduce the computation time.
