***
# Operationalizing Machine Learning
***
This project is part of Udaity Microsoft Azure ML Nanodegree program, which shows the code, screenshots, results and full video demostration of an operationalizing machine learning using Azure ML Studio, Azure SDK and Swagger.
***
***

# Project Overview
***
This project first begins with uploading the dataset which is about bank showcasing in which it contain a few subtleties of the clients like credit taken or not indicated as "advance" section and different subtleties like age, work title, conjugal status. The objective is to anticipate y section utilizing different highlights given in dataset we initially accomplish it utilizing autoML which do alot of preparing himself. I have used AutoML function on Azure to generate the best model using a metric and ending criteria. The model is then deployed using Azure ACI to generate a swagger URI and REST API endpoint.Using Azure and its workspace, this project looks at creating a cloud based machine learning model, from deployment to consumption and finally publication. Commands for the deployment, processing and endpoint results are executed using Git Bash.
The Architecture of project followed by step by step screeshots with description of working project mentioned below.
***

## Architectural Diagram
***
![Architecture Design](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/Project-Architecture.png)
***

## Key Steps
***
***
1. **Create an experiment using AutoML, register the dataset, configure a compute cluster, and use that cluster to run the experiment. On successfull completion best performing model will be returned.**
***
For registering dataset Go to Dataset and click on create dataset with web URL, give the web URL and a valid name for Dataset. 
![Registering Dataset step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/dataset-1.JPG)

Then in column headers I changed the value to "Use headers from the first file".
![Registering Dataset step 3:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/dataset-2.JPG)

Final result
![Final Registered Dataset](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/dataset-3.JPG)

After that I have created An AutoML Run and for that go to Automated ML click on crate an new Run and select the already registerd 'BankMarketing Dataset'. 
![AutoML experiment step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-1.JPG)

In The Experiment you can see the Experiment Run Status.
![AutoML experiment step 2:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-4.JPG)

Experiment Run & Best Model Summary
![Best Model Summary](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-2.JPG)
![Best Model Details](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/automl-3.JPG)
***

2. **Deployment of Best Performing Model**
***
Then I have deployed the best performing Model as You can see the deployed status in the below screenshot.
![Model Deployed step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/Model-deploy-1.JPG)
![Model Deployed step 1:](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/Model-deploy-2.JPG)
***

3. **Enable Log insights of the Endpoint**
***
I have enabled logs using logs.py script in which I have used "service.update(enable_app_insights=True)" to enable the logs in the deployed model endpoint.

This is the response I got after running logs.py
![log.py](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/enable-log-1.JPG)

This is the screen shot of my script
![log.py script](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/enable-log-2.JPG)
***

4. **Make documentation of deployed Endpoint using Swagger**
***
For setting up swagger I have first downloaded swagger.json file from deployed model endpoint and then I have pasted the swagger.json file in the folder where my script resides. 

Then I have run serve.py script which serves our json using python script. Below is the screen shot of serve.py result. 
![serve result](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/swagger-2.JPG)

Then I have pasted the url of json served using serve.py to swagger which is running on port 9000 and then I have checked the /score endpoint.
![Swagger API detail](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/swagger-3.JPG)

Below is the screen shot of scripts running to use swagger
![Swagger running](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/swagger-4.JPG)
***

5. **Consume the model endpoints and show benchmarks for the endpoint.**
***
For consuming the model I have pasted my score url and primary key in the endpoint.py file.
![Endpoint script](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/endpoints-1.JPG)

Then I have checked that whether I have az installed and then I have run endpoint.py in the command line which gave me the following result.
![Endpoint result](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/endpoints-2.JPG)

***
Benchmark
![Benchmarks 1](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/benchmark-1.JPG)
![Benchmarks 2](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/benchmark-2.JPG)
***

6. **Use Jupyter Notebook to create, publish and consume a pipeline.**
***
Registered Dataset "BankMarketing-Dataset"
![Dataset](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-dataset.JPG)
Published Pipeline Overview Graph 
![Published Pipeline Overview](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-4.JPG)
AutoML Pipeline Run details
![Run Details](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-1.JPG)
Running Pipeline Endpoints Run
![Pipeline Endpoints Run](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-3.JPG)
Published Pipeline Active Status
![Pipeline Endpoints Active](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-2.JPG)
Pipeline Endpoint
![Pipeline Endpoint](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-5.JPG)
Pipeline Scheduled Run
![Scheduled Run](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-6.JPG)
Pipeline RunDetails Widget
![RunDetails Widget](https://github.com/yash872/operationalizing-machine-learning/blob/master/Images/pipeline-7.JPG)
***

## Screen Recording
***
:movie_camera: [Click here for the Screencast](https://drive.google.com/file/d/180JqYjitLLWAOrU1sIijdsMxuXo47oPz/view)
***

## Standout Suggestions
***
1. We can modify the Training & Testing ratios of the Model for best distribution to get the best accuracies.
2. There are a lot of settings which can change to improve the hunt space and help to achive a far better model arrangement.
3. We can also Comparing the model results with a hyperdrive configuration model to identify which parameters are better at predicting the good output column values.
4. Generating more features from the dataset columns to make the models more open ended.
5. We can Add some visual to the swagger localhost endpoint to summarize the model's main findings.
***

*[Personal Recommendation]* :blush:
- I would also recommend you all to search for some different arrangements for labs as opposed to utilizing RDP gateway as it is irritating and bridle your advancement.

***
***
