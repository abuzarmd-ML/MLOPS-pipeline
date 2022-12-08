
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

## write scripts and utilities
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
