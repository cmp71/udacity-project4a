[![CircleCI](https://circleci.com/gh/cmp71/udacity-project4a.svg?style=shield)](https://app.circleci.com/pipelines/github/cmp71/udacity-project4a)

## Project Overview

Operationalize a Machine Learning Microservice API. 

I was given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. This project tested my ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls.  

There were numerous issues encountered in completing this project.  
Most were caused by environmental issues, for example, the directions as supplied may have worked on a Mac a year ago when the project was first created, but today it does not.  
Also the project requires a multiple vCPU system and considerable disk space, which took trial-and-error to discover.  
A detailed list of all attempts made can be found in the file `diary.md`.  
The final working attempt is **Attempt #6**  

### Summary of activities
* Setup environment in Amazon EC2
* Installed python3, docker, hadolint, pylint, kubectl, minikube
* Cloned provided repository from github
* Created and activated a python virtual environment
* Updated `Makefile`
* Ran `make install` to setup python environment
* Updated `Dockerfile`
* Ran `make lint` to lint the Dockerfile and python app
* Made some updates to the supplied app to score a 10/10 on linting
* Updated `run_docker.sh`
* Ran `run_docker.sh` to create and run a Docker image with the app
* Ran `make_prediction.sh` to test the Docker container and the app
  * Saved the output to `output_txt_files/docker_out.txt`
* Edited the python app to add additional console logging, re-built Docker image, deployed and tested
* Started minikube to create a local kubernetes cluster
* Updated `run_kubernetes.sh`
* Ran `run_kubernetes.sh` to deploy app to cluster and ran `make_prediction.sh` to test.
  * Saved the output to `output_txt_files/kubernetes_out.txt`
* Created new github repo (this one), configured local git environment, and pushed to this repo
* Added circleci integration

### Files in repo
app.py			The python app  
diary.md		Comprehensive notes  
Dockerfile		Dockerfile to build docker image with python app  
Makefile		To setup python environment and linting  
make_prediction.sh	Shell script to test the python app  
model_data		App data as supplied  
output_txt_files	Evidence of working app  
README.md		This  
requirements.txt	python environment dependencies  
run_docker.sh		Shell script to create and deploy a docker image with the python app
run_kubernetes.sh	Shell script to pull docker image and deploy to a kubernetes cluster
upload_docker.sh	Shell script to push docker image to docker hub

### Instructions
After setting up the environment:  
* `run_docker.sh` to build and deploy a docker image with the python app  
* In a separate terminal, run `make_prediction.sh` to test the deployed app

* `run_kubernetes.sh` to pull the docker image from docker hub and deploy to a kubernetes cluster
* In a separate terminal, run `make_prediction.sh` to test the deployed app
