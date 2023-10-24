<div align="center">

# xhec-mlops-project-student

[![CI status](https://github.com/artefactory/xhec-mlops-project-student/actions/workflows/ci.yaml/badge.svg)](https://github.com/artefactory/xhec-mlops-project-student/actions/workflows/ci.yaml?query=branch%3Amaster)
[![Python Version](https://img.shields.io/badge/python-3.9%20%7C%203.10-blue.svg)]()

[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)
[![Linting: ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/charliermarsh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![Pre-commit](https://img.shields.io/badge/pre--commit-enabled-informational?logo=pre-commit&logoColor=white)](https://github.com/artefactory/xhec-mlops-project-student/blob/main/.pre-commit-config.yaml)
</div>

This repository has for purpose to industrialize the [Abalone age prediction](https://www.kaggle.com/datasets/rodolfomendes/abalone-dataset) Kaggle contest.

### Team 4
**Arthur Perrigot - Théophile Lepic - Aristide Gasquet - Guillaume Plassais - Matthieu Marquis--Lorber - Guillaume d'Hérouville**

Respectively :
 - arthurprgt
 - tlepic
 - arigqt
 - gplassais
 - mattmrq
 - guillaumedherouville

<details>
<summary>Details on the Abalone Dataset</summary>

The age of abalone is determined by cutting the shell through the cone, staining it, and counting the number of rings through a microscope -- a boring and time-consuming task. Other measurements, which are easier to obtain, are used to predict the age.

**Goal**: predict the age of abalone (column "Rings") from physical measurements ("Shell weight", "Diameter", etc...)

</details>

## Clone the repository
```
git clone https://github.com/arthurprgt/xhec-mlops-project-student.git
cd xhec-mlops-project-student
```

## Run the Dockerfile from your computer

The role of the Docker image is to facilitate the industrialization, deployment, and hosting of the trained model as an API for prediction.

1. Make sure than you have Docker Desktop open on your computer.
2. Build the Docker image
```
docker build -t abalone_age -f Dockerfile.app .
```
3. Run the Docker container
```
docker-compose up -d
```
4. Try out the app
  - Check the workflows at http://localhost:4200
  - Try out the API at http://localhost:8001/docs


## Run the Dockerfile from Docker Hub

1. Make sure than you have Docker Desktop open on your computer.
2. Modify the docker-compose.yml: replace `abalone_age` with `adherouville/mlops_artefact:3`
3. Run the Docker container
```
docker-compose up -d
```
4. Try out the app
  - Check the workflows at http://localhost:4200
  - Try out the API at http://localhost:8001/docs


## Working on local computer

1. Create a virtual environment
```
conda env create --file environment.yml
conda activate x-hec-solution
```
2. Install requirements
```
pip install -r requirements.txt
pip install -e .
```
3. Running the workflows with Prefect
```
prefect config set PREFECT_API_URL=http://0.0.0.0:4200/api
```
```
prefect server start --host 0.0.0.0
```
```
python src/modelling/main.py
```
Check the workflows at http://localhost:4200

4. Running the API with uvicorn
```
uvicorn src.web_service.main:app --host 0.0.0.0 --port 8001
```
Try out the API at http://localhost:8001/docs
