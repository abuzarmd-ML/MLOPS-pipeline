
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
2. I have written all the steps in the yaml file for ci-cd
3. push this file on the github
4. Open Action tab in github repo, some action is getting performed automatically . That is continous integration of the code.

## Deploy this workflow on Heroku or other server.
1. I have deployed it on heroku. Due to monatery charges i have deleted the project from Heroku
