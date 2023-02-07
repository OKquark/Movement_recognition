# Movement_recognition
Educational project with SpineWise company.
The SpineWise company kindly provided their movement sensor data for processing and creating a model for human movements recognition. The main concept of the project is to recognize movements of employees, e.g.supermarkets (walking, types of bending, crouching,…). 

Especially harmful movements for the neck and the back should be detected. The recognition of workers activity enables the client to provide proactive recommendations and prevent the health damaging movements of workers. 

Using the available time series data and ML-techniques the **movements** will be **recognized and labeled**. In the notebook is used K-means Clustering for Time Series with Dynamic Time Warping.

## Getting Started

The **sensor data** are in unlabeled data in `csv` format. Each dataset captures values from 2 sensors placing on the neck and on the hip belt. 
The sensor data are the following: 
**measured values** x, y, z from accelerometer, gyroscope and magnetometer;
**calculated values** of alpha & beta comparatively to the neutral position of the person and kal_status indicating that a certain action is true or false.
The frequency is 25 measurements per second (25 Hz). There are round 700 000 - 800 000 measurements per dataset. 

## Prerequisites
* Python 3.x 
* pandas
* numpy
* scikit-learn 
* matplotlib
* seaborn
* from tslearn.metrics import soft_dtw
* from tslearn.clustering import TimeSeriesKMeans
* from tslearn.preprocessing import TimeSeriesScalerMeanVariance

## Installation

This step by step guide will get you to have the development environment up and running.

1. Create and activate your virtual environment
2. Install additional packages and libraries
3. Open the notebooks in a code editor of your choice running on the virtual environment you just created

## Usage

1. To create the model and define clusters run spinewise_cluster_Kmean_DTW_ok.ipynb 
2. The file spinewise_cluster_Kmean_DTW.ipynb contains also results with cluster numbers: 6, 9, 16. 

## Pipeline

1. **Analyse signals**
> The signals from the csv files do not allow visually recognize patterns or correlation between features to label the dataset. Magnetometer values are not taken into account in this project.

2. **Normalization**
> TimeSeriesScalerMeanVariance is a scaler used to pre-process time series data. The purpose of this scaler is to transform the time series data in a way that each time series has a mean of zero and a variance of 1. This is done to remove the influence of the amplitude of a time series and only focus on its shape for comparison purposes. This means that each time series is scaled independently and there is no overall data range, so the barycenters cannot be scaled back to the original data range. The goal is to compare the shapes of the time series in an amplitude-invariant manner and to ensure that no single modality contributes a large portion of the variance.    

3. **Building clustering model with noise reduction**
> In the notebook is used K-means Clustering for Time Series with Dynamic Time Warping. The goal of TimeSeriesKMeans with metric="softdtw" is to group similar time series together into clusters based on their similarity as measured by the soft DTW metric.

4. **Visualize clusters and clusters' centers**
> For better visualisation 7 clusters are plotted on the initial dataset reduced with 2 PCA(Principal Component Analysis).   

5. **Evaluate the model**
> The number of clusters is evaluated using Elbow method and silhouette_score metrics.

6. **Save the model for deployment**
> The model is saved using joblib library into .pkl format.

## Deployment

The end-result is currently being deployed into a spreadsheet (csv file).

## Contributors

1. [Olga Kuznetsova](https://github.com/OKquark) 


## Timeline

Project Start ---> `9 January 2023`  

Project End ---> `20 January 2023`
