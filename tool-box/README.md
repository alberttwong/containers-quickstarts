Sometimes you just need to manage or debug your MongoDB container environment or kubernetes cluster with MongoDB in it.   This container can launched inside or outside a kubernetes cluster and contains many of the tools you'll need to manage your MongoDB environment.  A sample use of this container could be the use case of performing tasks on a mongoDB cluster within a kubernetes cluster.   Instead of trying to connect to MongoDB from outside the kubernetes cluster, launch a container within the kubenetes cluster and run tasks from inside the cluster.     Another use case is that I don't want to install the mongoDB tools on my host.   In this case, just startup a container, use the tools and then exit the container.  No tools would be installed on the host. 


This project inherits from https://github.com/redhat-cop/containers-quickstarts/tree/master/tool-box

# What's in the box? 

oc version 4.4.7.   
ansible v2.9 (stable from pip).   
python v3.6.    
git 2.18.4.      
unzip 6.0-43.   
jq v1.6.    
odo 1.2.1.   
kubectl 1.18.     
helm Client v3.2.1.   
tkn Client v0.9.0.  
MongoDB CLI 1.8  
MongoDB Shell 0.5.0     
MongoDB Client 4.4.1   
MongoDB Tools 100.2       
If you need something not here, let us know in an issue or submit a PR at https://github.com/alberttwong/containers-quickstarts/blob/master/tool-box/Dockerfile


# Usage

## OpenShift

To run the container in OpenShift and get a shell, you have 2 options. First option is to go to the correct project `$ oc project` and run the container `$ oc run -i -t tool-box-mongo --image=atwong/tool-box --rm bash`.  Another option is to use the UI and use the service catalog to perform a container image deploy.  Next, navigate to the pod and then click on terminal to get a shell.   To delete the pod after using it, delete the deployment or deployment config.

## Docker

If you need sudo for docker: `$ sudo docker run -it atwong/tool-box /bin/bash` or if you don't need sudo: `$ docker run -it atwong/tool-box /bin/bash`

