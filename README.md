
# MLOPS-pipeline

This project is implementation of MLOPS pipeline. 
You can use the below steps in order to replicate the pipeline at your end.

## Create a virtual environment first

**For linux :**
  - use the command on the terminal:
    
    `mkvirtualenv mlops`

  - write the command to get in the virtual env:
    
    `workon mlops`

  **For Windows :**
  - Follow through the link below:
    
    [virtual environment on windows](https://medium.com/co-learning-lounge/create-virtual-environment-python-windows-2021-d947c3a3ca78)


## Create a template of the project.

Insted of making a project directory manually. use `template.py`
`python3 template.py`

## Perform the below steps in order to version control the data and code.
1. Download the dataset from:
 https://drive.google.com/file/d/1bJjVZ8eju8qu-JYzr_wOOL7DJa2RqZvk/view?usp=share_link 

or from kaggle.

2. Make directory  `mkdir data_given` and paste the dataset inside it.
3. Initialize the git repo 
`git init`

4. Initialize DVC:
`dvc init `

5. Add the data for tracking using dvc
`dvc add data_given/winequality.csv`

you will find the 1 more file after this step whose extension is .dvc (winequality.csv.dvc)

6. Add the code for tracking using git
`git add .`

`git commit -m "first commit"`

7. Make a README.md file (you can download from this repo)

  oneliner updates for readme

  `git add . && git commit -m "update Readme.md"`

## write scripts and utilities for Training
Perform below steps:

1. I have written `src/get_data.py` for uploading params file.

2. I have written `src/load_data.py` for preprocessing the dataset, like renaming column.
   processed dataset are saved in: `data/raw/winequality.csv`

3. write steps of pipeline execution in dvc.yaml file.

4. run below command to execute the pipeline:
`dvc repro`

5. I have written `src/split_data.py` to split the data set into train and test
   
   I have also added this step in `dvc.yaml`
   
   run: `dvc repro`
  
   push the changes to the github repo.

6. I have written `src/train_and_evaluate.py` for model prediction and estimation.
   To pass parametetrs to the model, all the parameters are added in `params.yaml` and all the pipeline parameters are added in `dvc.yaml`

   run: `dvc repro`
   push the changes to the github repo.

7. The prediction values and scores are stored in the `report/` folder. 
8. just change the value of parameters for estimators in `params.yaml`. 
   
   and run : `dvc repro`.
   
   run: `dvc metrics show` . It will give scores and param mapping
   
   run: `dvc metrics diff` . It will give difference of previous and current result

## Add Test Cases for project

1. Tox is a tool that creates virtual environments, and installs the configured dependencies for those environments, for the purpose of testing a Python package.
  
   Install tox:
    ```bash
      pip install tox
    ```
2. create a directory where we will write test cases.
    
    ```bash
      mkdir tests
      touch tests/conftest.py tests/test_config.py tests/__init__.py
    ```
3. Run Test cases as:

    ```bash
    pytest -v
    ```

## EDA on dataset

1. I have written `notebooks/EDA.ipynb` to perform EDA on the dataset and generated `schema_in.json` . This schema contains the min and max value of all the column, which will help us defining the range of the column.

## Add Web Structure 
1. I have created `prediction_service/` folder
2. I have created `webapp/` folder to design a simple webpage using flask.
3. I have written endpoint entry for webpage in `app.py` .
4. Enter the values in the range shown in the form otherwise 404 status code is generated.
5. I am not emphasizing on web development. Only added 1 webpage.

## Creating CI-CD pipeline for github action.

1. Create an action workflow for github at `.github/workflows/ci-cd.yaml`
2. I have written all the steps in the yaml file for continouous integration
3. push this file on the github
4. Open Action tab in github repo, some action is getting performed automatically . That is continous integration of the code.
## Load webpage

1. To run the webpage just execute: `python app.py`
2. In the console, there is a URL, copy and paste on the browser or Postman. you will get the webpage, where a page with form fill up will open
3. Enter the range of values suggested in the form, you will get the predicted output.
4. If any value is out of range, you will get the 404 error.

   Note: I have not created webpages in fancy manner. But, it will work.

## Deploy this workflow on Heroku or other server.
1. I have deployed it on heroku. Due to monatery charges i have deleted the project from Heroku

## MLFLOW
1. checkout a seperate branch for mlflow operations
  ```bash 
  git checkout -b mlflow
  ```
2. I have changed the `dvc.yaml` , `params.yaml` file

3. According to MLFLOW, I am changing `train_and_evaluate.py`
4. creating a folder `artifacts/` to save models and other artifacts.
5. Run below mlflow server command -
  ```bash
  mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./artifacts --host 0.0.0.0 -p 1234
  ```

6. On the web browser hit the url(in my case)- http://0.0.0.0:1234
7. On the browser you will get MLFLOW dashboard.
8. Initially, Dashboard is empty. As soon as you will run `dvc repro` on your terminal, Browser gets updated and you can see experiments on dashboard.
9. Do more experiments by changing parameters value in `params.yaml` .
10. run : `dvc repro`. 
11. as many number of time you will do the experiments, MLFLOW dashboard will be updated and all the reports will be logged on the dashboard.
12. In `artifacts/` folder also experiments are logged.
13. On the dashboard, you can do all the analysis of your model.
14. select whatever model you want to select according to the accuracy logged and click on artifacts->model and click `ElasticnetWineModel` (in our case).
15. click on `stage` dropdown, you will get options to deploy on production. 
16. Now, make ci-cd pipeline for this braanch also. 
17. push the changes to github
18. you can see all the action are performed in github succesfully.