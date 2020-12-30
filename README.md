# Udacity Project 2: Operationalizing Machine Learning

### Project Overview
For the second project of the Udacity Machine Learning Engineer with Microsoft Azure Nanodegree we were tasked with training and deploying models. The dataset that was used for this project was the 'bank marketing' dataset, where the goal is to use information about individuals to predict their receptiveness to additional marketing materials and products. Within this project I used Azure Machine Learning Studio's automated machine learning capabilities to train and test a variety of different models in order to find the most performant model. I then deployed the best model via an Azure Container Instance and tested the model's availability by submitting requests to it. Finally, a pipeline encompassing the process of creating an automated ML run with the bank marketing pipeline was created and published. 

### Automated Machine Learning
To begin the project, a new registered dataset was created by uploading the bank marketing dataset. Following the upload process the dataset is listed alongside other registered datasets.

![Registered bank marketing dataset](/images/registered-datasets.png)
