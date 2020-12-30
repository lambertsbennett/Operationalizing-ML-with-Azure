# Udacity Project 2: Operationalizing Machine Learning

### Project Overview
For the second project of the Udacity Machine Learning Engineer with Microsoft Azure Nanodegree we were tasked with training and deploying models. The dataset that was used for this project was the 'bank marketing' dataset, where the goal is to use information about individuals to predict their receptiveness to additional marketing materials and products. Within this project I used Azure Machine Learning Studio's automated machine learning capabilities to train and test a variety of different models in order to find the most performant model. I then deployed the best model via an Azure Container Instance and tested the model's availability by submitting requests to it. Finally, a pipeline encompassing the process of creating an automated ML run with the bank marketing pipeline was created and published. 

### Automated Machine Learning
To begin the project, a new registered dataset was created by uploading the bank marketing dataset. Following the upload process the dataset is listed alongside other registered datasets.

![Registered dataset](/images/registered-dataset.png)

Then, once the dataset was uploaded, I configured the automated machine learning run to carry out a classification experiment and specified the target variable. The experiment ran for approximately 1 hour and, following completion, you see the following:

![AutoML completed](/images/completed-automl.png)

After an hour of testing a variety of normalization schemes and classification algorithms the Voting Ensemble algorithm emerged as the best model with an accuracy of nearly 92%.

![Best autoML model](/images/best-model.png)

### Model Deployment
Following the AutoML run, the best model (Voting Ensemble) was deployed using an Aure Container Instance with authentication enabled. Next, using the SDK I enabled application insights for the deployed model. This change is reflected in the model overview as shown below:

![Application Insights](/images/app-insights-best-model.png)

The next task was to check log output from the deployed model. This was done using the supplied logs.py script. After running the script the following output was displayed:

![Logs](/images/logging-py-output.png)

Clearly shown in the log output are GET requests sent to the model to retrieve the swagger.json file that can be used to generate Swagger documentation. 

To verify that the containerized model's Swagger documentation is properly set up I then ran two provided scripts swagger.sh and serve.py. swagger.sh simply contains two Docker commands: 1) Pull the Swagger container image and 2) run the Swagger container with port forwarding.

serve.py creates a simple HTTP server to expose the swagger.json file to the Swagger container. After running these two scripts I navigated to localhost:8000/swagger.json and could view the generated documentation.

![Swagger](/images/swagger-documentation.png)

To test the availability of the deployed model, I used the provided endpoint.py script. The script simply sends a request containing two profiles of individuals for the model to predict whether they should be the target of additional marketing. The request is sent to the model's URI and authentication information is embedded in the request header. The response received from the model consists simply of a dictionary containing the description 'result' and the predictions for each individual sent in the request. (In this case No for both)

![Predictions](/images/Model-response-json.png)

### Pipeline Creation and Deployment
The second part of this project was to create, publish, and consume a pipeline using the Azure SDK. This was achieved using the provided Jupyter Notebook. Within the notebook the first step was to link the workspace and define an experiment. Then the compute cluster used previously was attached for the autoML run that was the central aim of the pipeline. Running all cells of the notebook resulted in a simple to represent pipeline:

![Pipeline](/images/pipeline-designer.png)

Within this pipeline the same bank marketing dataset is linked to an AutoML step allowing AutoML experiments to be run with ease. 
After running the notebook I carried out several checks to ensure that the pipeline was available:

1) I checked the pipeline section of ML Studio to make sure that the pipeline had been created successfully.
![Pipeline Created](/images/running-pipeline.png)

2) I checked that the pipeline had been published effectively and that the REST endpoint was available.
![Available Pipeline](/images/active-pipeline.png)

3) During the process of running the pipeline I monitored progress using the RunDetails Widget.
![RD widget](/images/widgets.png)

4) I checked that the REST endpoint was active and submitted a job using an HTTP request. I then checked that the job was running as expected.
![piplin](/images/running-pipeline2.png)
