# CloudComputingAndSecurity
## Image Object Detection API within a Containerised Environment
+ A python based web service that accepts images, uses YOLO and OpenCV to process images, and returns a
JSON response with a list of detected objects.
+ Built a Docker Image for the object detection web service.
+ Created a Kubernetes cluster on a virtual machine (instance) in the Nectar cloud.
+ Deployed a Kubernetes service to distribute inbound requests among pods that are running the object
detection service.
+ Tested the system under different load and number of pods.

### Steps: 1
#### Create an instance
Create an Ubuntu Instance in any cloud provider: Azure Ubuntu Instance, or EC2-Linux instance.
In the video instruction I have used Nectar Cloud Ubuntu Instance

### Steps: 2
#### Install Docker
first of all check if docker is installed or not

###### From Docker Repository
```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
```

#### Starting and Enabling docker service
On Ubuntu 18.04 the service is enabled and running after installation.
```
sudo systemctl enable docker
sudo systemctl start docker
```
#### Running docker commands as non-root user
```
getent group docker
sudo gpasswd -a <user> docker
getent group docker
```
Log out and log back in

Step 2 Source : https://github.com/justmeandopensource/learndocker/blob/master/INSTALL_Doc.md

### Step: 3
#### Install GO
```
wget https://golang.org/dl/go1.15.5.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.15.5.linux-amd64.tar.gz
```
Set Environment Variable
```
export PATH=$PATH:/usr/local/go/bin
```

### Step: 4
#### Install Kind (Kubernetes in docker)
```
GO111MODULE="on" go get sigs.k8s.io/kind@v0.9.0 
```
Source: https://github.com/kubernetes-sigs/kind
After download move go to the /usr/local/go/bin directory
``` 
sudo mv go/bin/kind /usr/local/go/bin/
```
By doing so, you have successfully installed kind. To validate:
``` 
kind version 
```
### Step: 5
#### Install Kubectl (Kubernetes command-line tool)
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.19.0/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
to confirm installation
```
kubectl version --client
```

### Step: 6
#### Create a Cluster

Clone the repo or download  
``` 
git clone https://github.com/Farhad-Rezwan/CloudComputingAndSecurity.git
```
Create cluster
```
cd CloudComputingAndSecurity
kind create cluster --config kindconfig.yml
```
To confirm cluster is created
```
kind get clusters
```
To confirm configuration of nodes:
```
kubectl get nodes

```
### Step: 7
#### Loading Docker image in the cluster:
```
cd iWebLens/webservice/server/
docker build -t my-custom-image .
kind load docker-image my-custom-image:latest
cd ../../k8sconfig/
kubectl apply -f iweblens_k8s.yml
```

### Step: 10
Allow inbound ports 30001, to make the web-service live in internet
### Step: 9
#### Test on your local machine

Download the client folder from the repo, and inside `inputfolder` add your image.
run the python command
```
python3 iWebLens_client.py  inputfolder  http://IP_ADDRESS_OF_INSTANCE:30001/api/object_detection 4
```
![](./demoImageDetection.gif)

### Video Instruction

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/ZgcaXSQksMQ/0.jpg)](https://www.youtube.com/watch?v=ZgcaXSQksMQ)

