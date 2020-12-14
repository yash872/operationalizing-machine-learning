***
# Operationalizing Machine Learning
***
This project is part of the Udacity Microsoft Azure ML Nanodegree program, which shows the code, screenshots, results, and full video demonstration of operationalizing machine learning using Azure ML Studio, Azure SDK, and Swagger.
***
# Project Overview
***
This project first begins with uploading the dataset which is about bank showcasing which it contains a few subtleties of the clients like credit is taken or not indicated as "advance" section and different subtleties like age, work title, conjugal status. The objective is to anticipate 'y' section utilizing different highlights given in the dataset we initially accomplish it utilizing AutoML which does a lot of preparing himself. I have used the AutoML function on Azure to generate the best model using a metric and ending criteria. The model is then deployed using Azure ACI to generate a swagger URI and REST API endpoint. Using Azure and its workspace, this project looks at creating a cloud-based machine learning model, from deployment to consumption and finally publication. Commands for the deployment, processing, and endpoint results are executed using Git Bash.
The Architecture of the project followed by step-by-step screenshots with a description of the working project mentioned below.
***

## Architectural Diagram
***
![Architecture Design](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/Project-Architecture.png)
***

## Key Steps
***
**Step-1. Uploading Data and Authentication**
***
The project begins by launching the main studio and uploading the dataset from the link(https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv). After specifying a computer cluster with a minimum number of nodes and the target column to be predicted, the dataset and its run is set up in the workspace. These can be seen from the figures below
![Registering Dataset step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/dataset-1.JPG)

Then in column headers, I changed the value to "Use headers from the first file", so that the valid columns will be used throughout the whole Dataset.
![Registering Dataset step 3:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/dataset-2.JPG)

Here you can see that our "Bankmarketing-Dataset" is successfully created and registered.
![Final Registered Dataset](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/dataset-3.JPG)
***

**Step-2. Using AutoML and Generating Model**
Now for generating the Model, we have to create an AutoML run and give that our registered Dataset which is 'Bankmarketing-Dataset'.
![AutoML experiment step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-1.JPG)

we run an experiment using the cluster and use that cluster to run the experiment. From the figures below we can see that VotingEnsemble produces the best accuracy after repeated runs. This step is crucial to choose and determine the best model through the AutoML function, before shipping the model into production.
In the Experiment, you can see the Experiment Run Status.
![AutoML experiment step 2:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-4.JPG)

Experiment Run & Best Model Summary
![Best Model Summary](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-2.JPG)
![Best Model Details](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-3.JPG)
***

**Step-3. Deployment of Best Performing Model**
***
In order to create an undisturbed cloud platform that can communicate seamlessly with the backend, authentication is important. Continuous Integration and Delivery systems (CI/CD) require a well-authenticated system that can automate the logging in process, either through passwords or tokens. The ACI container system is used for the scope of this project.
![Model Deployed step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/Model-deploy-1.JPG)
![Model Deployed step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/Model-deploy-2.JPG)
***

**Step-4. Enable Log insights of the Endpoint**
***
After deploying the best model, we can check the deployment logs of the model and enable Application Insights by clicking on a check-box. For the purpose of the project, however, this is enabled by executing the logs.py python file through GitBash.
I have enabled logs using logs.py script in which I have added "service.update(enable_app_insights=True)" to enable the logs in the deployed model endpoint.

This is the response I got after running logs.py
![log.py](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/enable-log-1.JPG)

This is the screenshot of the modified 'log.py' script
![log.py script](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/enable-log-2.JPG)

The deployment process involves delivering a trained model into production and then consuming it by clicking on the options in the endpoints section. For the purpose of this project, the deployment is done through the Azure ML Workspace, but it can also be done through the Python SDK. Model metrics with explanations can be seen in the figures and the screencast. The Best Model will be displayed in the Details tab. On deploying the Best Model, we can interact with the HTTP API service and interact by sending data over POST requests.
Azure Portal UI screenshot for depicting the Application Insights is enabled
![log.py script](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/enable-log-3.png)
***

**Step-5. Make documentation of deployed Endpoint using Swagger**
***
On deploying the model and enabling the application insights, we can now use Swagger to consume the endpoint. Azure provides a Swagger JSON file for deployed models. We first access the deployed model through the Endpoints section and save it in the Exercise folder. In the same folder, the swagger.sh will download the latest Swagger container, and it will run it on port 80. Due to connection issues, this was changed to 9000. The serve.py will start a Python server on port 8000
For setting up swagger I have first downloaded swagger.json file from the deployed model endpoint and then I have pasted the swagger.json file in the folder where my script resides.

Then I have run the serve.py script which serves our JSON using python script. Below is the screenshot of the serve.py result.
![serve result](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/swagger-2.JPG)

Then I have pasted the URL of JSON served using serve.py to swagger which is running on port 9000 and then I have checked the /score endpoint.
![Swagger API detail](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/swagger-3.JPG)

Below is the screenshot of scripts running to use swagger
![Swagger running](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/swagger-4.JPG)
***

**Step-6. Consume the model endpoints**
***
The logging process is used to help in the identification of issues and to visualize the performance of the model deployed. We can better interpret the access and use of the endpoint by looking at the Application Insights tab which can be modified through the Azure SDK. In this step, we execute the endpoint.py script to interact with the trained model. We then run the shell script, modifying both the scoring_uri and the key to match the key for the service and the URI. Information for the URI can be obtained through the Details tab, above the Swagger URI.
![Endpoint script](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/endpoints-1.JPG)

The deployed service is then consumed using an HTTP API, which generates a URL. The HTTP POST method used in this step is a way of submitting data. On consuming the endpoints by using the swagger commands and running the bash file, we get the results to show in the following figures which match with the project requirements.
![Endpoint result](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/endpoints-2.JPG)

***
**Step-7. Benchmark Run**
***
Apache Benchmark (ab) runs against the HTTP API using authentication keys to retrieve performance results.
![Benchmarks 1](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/benchmark-1.JPG)
![Benchmarks 2](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/benchmark-2.JPG)
***

**Step-8. Use Jupyter Notebook to create & publish the pipeline.**
***
**Registered Dataset "BankMarketing-Dataset"**
![Dataset](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-dataset.JPG)
**Published Pipeline Overview Graph**
![Published Pipeline Overview](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-4.JPG)
**Published Pipeline Active Status**
![Published Pipeline Active Status](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/Pipeline-Active.png)
**AutoML Pipeline Run details**
![Run Details](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-1.JPG)
For this part of the project, we use the notebook in the Exercise files to perform the same operations in the above steps to upload data, generate an AutoML model, deploy and create an endpoint using a URI, cluster and REST API point.
![Pipeline Endpoints Run](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-3.JPG)
**Published Pipeline Active Status**
![Pipeline Endpoints Active](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-2.JPG)
The figure below shows the result of a completed endpoint from the Jupyter files. More information can be seen through the screencast.
![Pipeline Endpoint](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-5.JPG)
**Pipeline Scheduled Run**
![Scheduled Run](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-6.JPG)
The pipeline is used as a stepping stone to automate model building and make the model publicly available for others to view and implement. For this project, the pipeline publishing process is by creating a computing instance with a specific number of nodes and endpoints. Once the endpoint is deployed and running, we can open Jupyter Notebooks and execute the cells to publish the model. The end result of this step is the creation of a public HTTP endpoint that can be accessed publicly once executed to success completely.
**Pipeline RunDetails Widget**
![RunDetails Widget](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-7.JPG)
***

## Screen Recording
***
:movie_camera: [Click here for the Screencast](https://drive.google.com/file/d/180JqYjitLLWAOrU1sIijdsMxuXo47oPz/view)
***

## Standout Suggestions
***
1. We can modify the Training & Testing ratios of the Model for the best distribution to get the best accuracies.
2. There are a lot of settings that can change to improve the hunt space and help to achieve a far better model arrangement.
3. We can also Comparing the model results with a hyperdrive configuration model to identify which parameters are better at predicting the good output column values.
4. Generating more features from the dataset columns to make the models more open-ended.
5. We can Add some visuals to the swagger localhost endpoint to summarize the model's main findings.
***

*[Personal Recommendation]* :blush:
- I would also recommend you all to search for some different arrangements for labs as opposed to utilizing the RDP gateway as it is irritating and bridle your advancement.

***
***
