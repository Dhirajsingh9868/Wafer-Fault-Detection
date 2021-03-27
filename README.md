
# Building a Machine Learning classification methodology to predict the quality of wafer sensors based on the given training data. 

# Data Description
The data is in multiple sets of files in batches at a given location. Data contais Wafer names and 590 columns of different sensor values for each wafer. The last column will have the "Good/Bad" value for each wafer.
"Good/Bad" column will have two unique values +1 and -1.  
"+1" represents Bad wafer.
"-1" represents Good Wafer. 
There is a "schema" file, which contains all the relevant information about the training files such as:
Name of the files, Length of Date value in FileName, Length of Time value in FileName, Number of Columns, Name of the Columns, and their datatype.

# Data Validation Validation
In this step, we perform different sets of validation on the given set of training files.  

# Model Training

1) Clustering - KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using "KneeLocator" function. The idea behind clustering is to implement different algorithms
   To train data in different clusters. The Kmeans model is trained over preprocessed data and the model is saved for further use in prediction.

2) Model Selection - After clusters are created, we find the best model for each cluster. We are using two algorithms, "Random Forest" and "XGBoost". For each cluster, both the algorithms are passed with the best parameters derived from GridSearch. We calculate the AUC scores for both models and select the model with the best score. Similarly, the model is selected for each cluster. All the models for every cluster are saved for use in prediction.
 
 
 # Prediction 
 
1) Data Export from Db - The data in the stored database is exported as a CSV file to be used for prediction.
2) Data Preprocessing    
   a) Checking for null values in the columns. If present, impute the null values using the KNN imputer.
   b) Checking if any column has zero standard deviation, remove such columns as we did in training.
3) Clustering - KMeans model created during training is loaded, and clusters for the preprocessed prediction data is predicted.
4) Prediction - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.
5) Once the prediction is made for all the clusters, the predictions along with the Wafer names are saved in a CSV file at a given location and the location is returned to the client.
 


 

