# project12
Data Scientist Nanodegree
Data Engineering
Project: Disaster Response Pipeline
Table of Contents
Project Overview
Project Components
ETL Pipeline
ML Pipeline
Flask Web App
Running
Data Cleaning
Training Classifier
Starting the Web App
Conclusion
Files
Software Requirements
Credits and Acknowledgements

1. Project Overview
In this project, I'll apply data engineering to analyze disaster data from Figure Eight to build a model for an API that classifies disaster messages.

data directory contains a data set which are real messages that were sent during disaster events. I will be creating a machine learning pipeline to categorize these events so that appropriate disaster relief agency can be reached out for help.

This project will include a web app where an emergency worker can input a new message and get classification results in several categories. The web app will also display visualizations of the data.

Here are a few screenshots of the web app.


2. Project Components
There are three components of this project:


2.1. ETL Pipeline
File data/process_data.py contains data cleaning pipeline that:

Loads the messages and categories dataset
Merges the two datasets
Cleans the data
Stores it in a SQLite database

2.2. ML Pipeline
File models/train_classifier.py contains machine learning pipeline that:

Loads data from the SQLite database
Splits the data into training and testing sets
Builds a text processing and machine learning pipeline
Trains and tunes a model using GridSearchCV
Outputs result on the test set
Exports the final model as a pickle file

2.3. Flask Web App

Running this command from app directory will start the web app where users can enter their query, i.e., a request message sent during a natural disaster, e.g. "Please, we need tents and water. We are in Silo, Thank you!".

Screenshot 1

master

What the app will do is that it will classify the text message into categories so that appropriate relief agency can be reached out for help.

Screenshot 2

results


3. Running
There are three steps to get up and runnning with the web app if you want to start from ETL process.


3.1. Data Cleaning
Go to the project directory and the run the following command:

python data/process_data.py data/disaster_messages.csv data/disaster_categories.csv data/DisasterResponse.db
The first two arguments are input data and the third argument is the SQLite Database in which we want to save the cleaned data. The ETL pipeline is in process_data.py.

DisasterResponse.db already exists in data folder but the above command will still run and replace the file with same information.

Screenshot 3

process_data


3.2. Training Classifier
After the data cleaning process, run this command from the project directory:

python models/train_classifier.py data/DisasterResponse.db models/classifier.pkl
This will use cleaned data to train the model, improve the model with grid search and saved the model to a pickle file (classifer.pkl).

classifier.pkl already exists but the above command will still run and replace the file will same information.

Screenshot 4

train_classifier_1

It took me around 4 minutes to train the classifier with grid search.

When the models is saved, it will look something like this.


Screenshot 5

train_classifier_2.jpg


3.3. Starting the web app
Now that we have cleaned the data and trained our model. Now it's time to see the prediction in a user friendly way.

Go the app directory and run the following command:


python run.py
This will start the web app and will direct you to a URL where you can enter messages and get classification results for it.

Screenshot 6

web_app


4. Conclusion
Some information about training data set as seen on the main page of the web app.

Screenshot 7

genre

Screenshot 8

dist

As we can see the data is highly imbalanced. Though the accuracy metric is high (you will see the exact value after the model is trained by grid search, it is ~0.94), it has a poor value for recall (~0.6). So, take appropriate measures when using this model for decision-making process at a larger scale or in a production environment.


5. Files
.
├── app
│   ├── run.py------------------------# FLASK FILE THAT RUNS APP
│   ├── static
│   │   └── favicon.ico---------------# FAVICON FOR THE WEB APP
│   └── templates
│       ├── go.html-------------------# CLASSIFICATION RESULT PAGE OF WEB APP
│       └── master.html---------------# MAIN PAGE OF WEB APP
├── data
│   ├── DisasterResponse.db-----------# DATABASE TO SAVE CLEANED DATA TO
│   ├── disaster_categories.csv-------# DATA TO PROCESS
│   ├── disaster_messages.csv---------# DATA TO PROCESS
│   └── process_data.py---------------# PERFORMS ETL PROCESS
├── img-------------------------------# PLOTS FOR USE IN README AND THE WEB APP
├── models
│   └── train_classifier.py-----------# PERFORMS CLASSIFICATION TASK


6. Software Requirements
This project uses Python 3.6.6 and the necessary libraries are mentioned in requirements.txt. The standard libraries which are not mentioned in requirements.txt are collections, json, operator, pickle, pprint, re, sys, time and warnings.


7. Credits and Acknowledgements
Thanks Udacity for letting me use their logo as favicon for this web app.

Another blog post was a great motivation to improve my documentation. This post discusses some of the cool projects from Data Scientist Nanodegree students. This really shows how far we can go if we apply the concepts learned beyond the classroom content to build something that inspire others.
