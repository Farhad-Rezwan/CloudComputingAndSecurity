# CloudComputingAndSecurity
## Steps: 1.
### Create an instance
Here we have used an Azure Ubuntu Instance

## Steps: 2.
### Install Docker:
first of all ckeck if docker is installed or not

### Ubuntu 18.04
###### From Docker Repository
```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
```
Docker service enabled and running by default
###### Using Convenienct Script from Docker
```
curl -fsSL https://get.docker.com | sudo sh -
```
## Starting and Enabling docker service
On Ubuntu 18.04 the service is enabled and running after installation.
```
sudo systemctl enable docker
sudo systemctl start docker
```
## Running docker commands as non-root user
```
getent group docker
sudo gpasswd -a <user> docker
getent group docker
```
Log out and log back in

Source : https://github.com/justmeandopensource/learndocker/blob/master/INSTALL_Doc.md

## Step: 3.
### Install GO.
```
wget https://golang.org/dl/go1.15.5.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.15.5.linux-amd64.tar.gz
```
set Environment Variable
export PATH=$PATH:/usr/local/go/bin

## Step: 3
Install Kind (Kubernetes in docker)
```GO111MODULE="on" go get sigs.k8s.io/kind@v0.9.0 ```
source: https://github.com/kubernetes-sigs/kind
After download move go to the /usr/local/go/bin directory
``` sudo mv go/bin/kind /usr/local/go/bin/```
By doing so, you have successfully installed kind. to check
``` kind version ```


[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/ZgcaXSQksMQ/0.jpg)](https://www.youtube.com/watch?v=ZgcaXSQksMQ)
