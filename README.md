
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

8. 


