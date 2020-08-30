# Project Diary
This file logs all the attempts to get Project 4 completed.  
If you are following this as a guide, Attempt #6 is currently the best option.

## Attempt #1. AWS Cloud 9
* Create environment, t2.micro (1 GiB RAM + 1 vCPU), Amazon Linux
* git clone
* Create python env
* make install
* Docker already installed
  * _Docker version 19.03.6-ce, build 369ce74_
* Install hadolint via docker
  * `docker run --rm -i hadolint/hadolint < Dockerfile`
  * Replaced hadolint line in Makefile with the above
  * `make lint` errors on app.py
    * https://pastebin.pl/view/fa8b3925
* Install kubectl
  * `curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"`
  * `chmod +x ./kubectl`
  * `sudo mv ./kubectl /usr/local/bin/kubectl`
  * `kubectl version --client`
    * _Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.0", GitCommit:"e19964183377d0ec2052d1f1fa930c4d7575bd50", GitTreeState:"clean", BuildDate:"2020-08-26T14:30:33Z", GoVersion:"go1.15", Compiler:"gc", Platform:"linux/amd64"}_
* Install minikube
  * `curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
  * `chmod +x minikube`
  * `sudo mkdir -p /usr/local/bin/`
  * `sudo install minikube /usr/local/bin/`
* Start minikube
  * `minikube start --driver=docker`
  * Fails, not enough vCPU's
    * https://pastebin.pl/view/b3d73d98
      
## Attempt #2. AWS Cloud 9
* Create environment, m5.large (8 GiB RAM + 2 vCPU), Amazon Linux
* git clone
* Create python env
* make install
* Docker already installed
  * _Docker version 19.03.6-ce, build 369ce74_
* Install hadolint via docker
  * `docker run --rm -i hadolint/hadolint < Dockerfile`
  * Replaced hadolint line in Makefile with the above
  * `make lint` errors on app.py
    * https://pastebin.pl/view/fa8b3925
* Install kubectl
  * `curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"`
  * `chmod +x ./kubectl`
  * `sudo mv ./kubectl /usr/local/bin/kubectl`
  * `kubectl version --client`
    * _Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.0", GitCommit:"e19964183377d0ec2052d1f1fa930c4d7575bd50", GitTreeState:"clean", BuildDate:"2020-08-26T14:30:33Z", GoVersion:"go1.15", Compiler:"gc", Platform:"linux/amd64"}_
* Install minikube
  * `curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
  * `chmod +x minikube`
  * `sudo mkdir -p /usr/local/bin/`
  * `sudo install minikube /usr/local/bin/`
* Start minikube
  * `minikube start --driver=docker`
  * Fails, "no space left on device"
    * https://pastebin.pl/view/38e1d026
  * Possible follow-up action > increase nvme partition size > https://stackoverflow.com/questions/52508038/how-to-increase-aws-ebs-nvme-size
    * _(.devops) ec2-user:~/environment/DevOps_Microservices/project-ml-microservice-kubernetes (master) $ sudo growpart /dev/nvme0n1 1_
    * _NOCHANGE: disk=/dev/nvme0n1 partition=1: size=20967390, it cannot be grown_

## Attempt #3. AWS Cloud 9
* Create environment, m5.large (8 GiB RAM + 2 vCPU), Ubuntu Server 18.04 LTS
* git clone
* Create python env
* make install
* Docker already installed
  * _Docker version 19.03.12, build 48a66213fe_
* Install hadolint via docker
  * `docker run --rm -i hadolint/hadolint < Dockerfile`
  * Replaced hadolint line in Makefile with the above
  * `make lint` errors on app.py
    * https://pastebin.pl/view/fa8b3925
* Install kubectl
  * `curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"`
  * `chmod +x ./kubectl`
  * `sudo mv ./kubectl /usr/local/bin/kubectl`
  * `kubectl version --client`
    * _Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.0", GitCommit:"e19964183377d0ec2052d1f1fa930c4d7575bd50", GitTreeState:"clean", BuildDate:"2020-08-26T14:30:33Z", GoVersion:"go1.15", Compiler:"gc", Platform:"linux/amd64"}_
* Install minikube
  * `curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
  * `chmod +x minikube`
  * `sudo mkdir -p /usr/local/bin/`
  * `sudo install minikube /usr/local/bin/`
* Start minikube
  * `minikube start --driver=docker`
    * Fails, "no space left on device"
      * https://pastebin.pl/view/69d885c4

## Attempt #4. MacBook Air
* macOS Catalina Version 10.15.6
* List of packages installed on this MacBook https://pastebin.pl/view/61f2348c
* git clone
* Create python env
* ➜  project-ml-microservice-kubernetes git:(master) `which python3`
* _/usr/bin/python3_
* ➜  project-ml-microservice-kubernetes git:(master) `python3 --version`
* _Python 3.8.2_
* `make install` errors
  * https://pastebin.pl/view/4a5b9db6
* Edited requirements.txt to remove all the hardcoded version numbers
  * This time `make install` completed successfully
* Installed pylint with `pip install pylint`
* Linting of the supplied app.py generates issues:
  * https://pastebin.pl/view/7661b074
  * Fixed joblib import issue
    * Replaced `from sklearn.externals import joblib` with `import joblib`
  * Fixed f-string issue
    * Replaced `html = f"<h3>Sklearn Prediction Home</h3>"` with `html = "<h3>Sklearn Prediction Home</h3>"`
* Updated Dockerfile and linted
* Updated run_docker.sh. Python errors when running docker run:
  * https://pastebin.pl/view/d2f593f8
  * This appears to be something to do with incompatible versions of scikit-learn which is beyond my knowledge to fix (and should be outside the scope of this course)

## Attempt #5. Windows 10 Laptop
* Windows 10 Home, OS Build 19041.450
* List of installed programs: https://pastebin.pl/view/69b3af5b
* Using git bash, git clone
* python cannot be run from command line
  * chris@HP-ENVYD6 MINGW64 ~/DevOps_Microservices/project-ml-microservice-kubernetes (master)
  * $ `python3 -m venv ~/.devops`
  * _bash: /c/Users/chris/AppData/Local/Microsoft/WindowsApps/python3: Permission denied_
* Tried a variety of fixes suggested on the internet (most involved reconfiguring $PATH) to no avail.

## Attempt #6. AWS EC2 Linux
* Create instance with Amazon Linux 2 AMI, t2.large (2 vCPUs, 8 GiB), raised disk from 8 GiB to 16 GiB
* `sudo yum update`
* Install git `sudo yum install git`
* git clone
* Install python3 `sudo yum install python3 -y`
* Create python env
* make install
* Install docker `sudo amazon-linux-extras install docker`
  * (.devops) [ec2-user@ip-172-31-2-30 project-ml-microservice-kubernetes]$ `docker --version`
  * _Docker version 19.03.6-ce, build 369ce74_
* Start docker daemon `sudo service docker start`
* Add permission for docker `sudo usermod -a -G docker ec2-user`
* Install hadolint via docker
  * `docker run --rm -i hadolint/hadolint < Dockerfile`
  * Replaced hadolint line in Makefile with the above
* Install pylint `pip install pylint`
* `make lint` errors on app.py, only the f-string issue previously seen. Fixed as before.
* Install kubectl
  * `curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"`
  * `chmod +x ./kubectl`
  * `sudo mv ./kubectl /usr/local/bin/kubectl`
  * `kubectl version --client`
    * _Client Version: version.Info{Major:"1", Minor:"19", GitVersion:"v1.19.0", GitCommit:"e19964183377d0ec2052d1f1fa930c4d7575bd50", GitTreeState:"clean", BuildDate:"2020-08-26T14:30:33Z", GoVersion:"go1.15", Compiler:"gc", Platform:"linux/amd64"}_
* Install minikube
  * `curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
  * `chmod +x minikube`
  * `sudo mkdir -p /usr/local/bin/`
  * `sudo install minikube /usr/local/bin/`
* Start minikube
  * `minikube start --driver=docker`
    * Success: https://pastebin.pl/view/7a82fb3d
* Update Dockerfile: https://pastebin.pl/view/ed1c0b2b
* Update run_docker.sh: https://pastebin.pl/view/227bfc8f
  * Success. App is waiting for input
* Edit make_prediction.sh, change PORT to 80
* `./make_prediction.sh` - Success
* Edit make_prediction.sh to add extra logging. Lint: success
* Re-run `./run_docker.sh` to rebuild image with new app.py
* Re-run `./make_prediction.sh` - Success
* `docker login`
* Update 'upload_docker.sh'
* Updated `run_kubernetes.sh`
  * Note, the port forwarding command at the end of the script fails as it executes too soon, need some kind of delay or checked loop to wait until the pod has been created and started
  * When pod started, running port forwarding command manually gives a permission denied error : https://pastebin.pl/view/1243bce3
  * Could be that something else already listening on 80... 
    * Changed to 8000:80
    * (.devops) [ec2-user@ip-172-31-2-30 project-ml-microservice-kubernetes]$ `kubectl port-forward udacity-project4 8000:80`
    * Started successfully
    * Update make_prediction.sh to poll port 8000 instead of 80
    * Successfully made prediction.
* Deleted minikube cluster with `minikube delete
* Upload to github
  * Generated local keypair with `ssh-keygen`
  * Added .ssh/id_rsa.pub to github
  * `git init`
  * `git remote add origin git@github.com:cmp71/udacity-project4a.git`
  * `git push --set-upstream origin master`
    * Error due to attempt to publish private email address: https://pastebin.pl/view/3340546a
    * Fix:
      * `git config --global user.email "12956104+cmp71@users.noreply.github.com”`
      * `git commit --amend --reset-author`
        * Opens a text editor for the commit message. Save and exit
      * `git log` to check the new no-reply email address is in place
  * `git push --set-upstream origin master` now works
