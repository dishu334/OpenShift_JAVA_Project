# OpenShift_JAVA_Project

OPEN Shift Tutorials
OpenShift Origin is based on top of Docker containers and the Kubernetes cluster manager, with added develop and operational centric tools that enable rapid application development, deployment and lifecycle management 

Docker: enable us to create an image of all the required dependencies which can instantly deployed in any environment.
Kubernetes: enable deployment and management of these docker images across large cluster by providing self and healing and autoscaling feature.

Kubernetes or K8s
Orchestration tool ansible
Container + Orchestration
First we need to understand these two term then we will be able to understand what Kubernetes do.
Containers:
Why do you need containers?
Dependencies of the services on library.
Compatibility/ Dependency
Long setup Time
Different env 
  


What are containers ??
Containers are completely insolated environment having sperate environment setup and network mount.

 Before I start explaining you about the containers lemme explain you how os works.
Os kernel acts like a layer btw the hardware and software running on it.
Here kernels remains the same it’s a software above it that make a system different.
Sharing the kernel : what does it actually mean lets we have a system ubuntu with docker installed on it 
Docker can run any flavor of os on top of it as long a it based on same kernel.
Docker utilize the underlying docker host which work with all the operating system above.
The main aim of dockerization is to containerize the application and make them sit.
 


 

Vm have complete isolation from each other’s not like docker.
Docker Images (Package Templates Plan): Used to create one or more containers 
Containers are the running instant of images that are isolated and have their own environment and set of process. 


Container Orchestration:
Now we are going to talk about container orchestration.
Example : what if your application relies on other docker images like database or messaging services containers, etc. And the number of user increases then we need to scale up the application.
The whole process of automatically deploying and managing containers is known as container Orchestration.
Kubernetes – google 
Mesos – Apache

Advantage of Kubernetes:
Multiple instant of application running on different nodes 
Depend Increases deployed more instant of application --- scale up and down automatically
 


OpenShift Architecture 
It leverage Kubernetes as a underlying structure.
We can deploy application in th form of containers.
Containers are created from images of application
Now  the question- from where do they docker images come from 
You can configure openShift to pull these images from public docker repositories or registry like docker hub.
We can make use of OCR (OpenShift Container Registry)  that comes build in with openShift.
A collection of one or more containers forms a POD and multiple PODS form a deployement.
And we use services to exposure the deployment to other application and outside world
 

To make all of these OpenShift comes with build in web console. Developer can easily access it and manage their application 
User can create application.
OpenShift also comes with build In SCM (Source code management system) thru which user can import their application code.
The code repository has integration with CI/CD pipelines where the application code is build into docker images and pushed into build in container registry.
 

At the heart of openshift – etcd ( key value stores) that stores the information  about various components. 
 
Many nodes are managed by one or more master nodes. Master host the api server and etcd
Setup OpenShift
1)	All in one (MiniShift) – master and child  node  - local system
2)	Single Master Multiple Nodes – for QA env
3)	Multiple master and multiple node -for prod
Installing and deploying open shift :
1)	Traditionally method of installation using RPM
2)	Thru container technology like Docker 

MiniShift
All-in-one
Components
	Kubernetes
	Etcd
	Openshift
All of the above components are bounded into single images 
 

https://www.okd.io/minishift/


Management Tools
•	Web console
•	CLI
•	Rest API
Web Console
Accessible at 8443 on default IP address 
 

Project View : where you configure and manage application view 


In window 10 we make use of Hyper V to run the openShift. 
 It lets you create and run a software version of a computer, called a virtual machine. 
 

CLI tools
It comes prepackage with minishift utility 
Just how you login into web portal similar u have to login using cli tools
Commands lines:
	oc login
	oc login -u developer -p password
 

3 Using Rest api

 


Setup Setups
https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html#for-windows

https://wiki.aciworldwide.com/display/BLR/Minishift+Windows+10+setup



commands :
minishift start --show-libmachine-logs -v5
https://github.com/minishift/minishift/issues/1656

MiniShift Cheat Sheet 
https://cheatsheet.dennyzhang.com/cheatsheet-minishift-a4
Web console
Users
 

 












To check all projects under system Login user …..
Note: You can see the all project under name of normal or other username thru UI
Thur CLI you can see the admin user and the set of all projects
 


Error cos of github:
C:\minishift\minishift-1.34.2-windows-amd64>minishift start --show-libmachine-logs -v5
-- minishift version: v1.34.2+83ebaab
-- Starting profile 'minishift'
Found binary path at minishift.exe
Launching plugin server for driver hyperv
Plugin server listening at address 127.0.0.1:64067
() Calling .GetVersion
Using API Version  1
() Calling .SetConfigRaw
() Calling .GetMachineName
(minishift) Calling .GetState
(minishift) DBG | [executing ==>] : C:\windows\System32\WindowsPowerShell\v1.0\powershell.exe -NoProfile -NonInteractive ( Hyper-V\Get-VM minishift ).state
(minishift) DBG | [stdout =====>] :
-- Check if deprecated options are used ... (minishift) DBG | [stderr =====>] : Hyper-V\Get-VM : Hyper-V was unable to find a virtual machine with name "minishift".

   Use of HYPERV_VIRTUAL_SWITCH has been deprecated
   Please use: minishift config set hyperv-virtual-switch External VM Switch
FAIL
(minishift) DBG | At line:1 char:3

(minishift) DBG | + ( Hyper-V\Get-VM minishift ).state
-- Checking if https://github.com is reachable ... (minishift) DBG | +   ~~~~~~~~~~~~~~~~~~~~~~~~
(minishift) DBG |     + CategoryInfo          : InvalidArgument: (minishift:String) [Get-VM], VirtualizationException
(minishift) DBG |     + FullyQualifiedErrorId : InvalidParameter,Microsoft.HyperV.PowerShell.Commands.GetVM
(minishift) DBG |
(minishift) DBG |
OK
-- Checking if requested OpenShift version 'v3.11.0' is valid ...
   Hit github rate limit: GET https://api.github.com/repos/openshift/origin/releases/tags/v3.11.0: 403 API rate limit exceeded for 161.69.112.11. (But here's the good news: Authenticated requests get a higher rate limit. Check out the documentation for more details.) [rate reset in 10m18s]
FAIL


To get rid of this error:

	minishift delete --clear-cache
	minishift start --show-libmachine-logs -v5


CLI oc command line tools

First Step  you need to set the oc to environment variable;

Go to minishift folder run >minishift oc-env

Commands:
	oc login -u system:admin   (* admin has access to all projects including the default projects)
	


API’s
 

oc login -u developer -p developer
oc whoami -t (* to get the token)
 



 


When user is logged in as system admin user:

oc login -u system:admin   

oc get projects

oc get users

to make admin user for console

oc adm policy add-cluster-role-to-user cluster-admin <username>
 




Builds & Deployments

Openshift create the automatically build job using the repo url specified while creating project 
 

It also deploy the application using the building kubernets structure 
It uses internal API’s to host the application
 

 
 	Builds

Pre-Requisites:
YAML Files
 

Build strategy can be of 2 type :
1 – Docker Build
2 – Source to Image(S2I)   directly converting the source code to image (*build in PRE BUILD python code)
3- Custom Build 


2- 
 


 


Error due to image stream tag reader for this you need to create new input stream reader 


Sample -> build-definition.yml

apiVersion: build.openshift.io/v1
kind: BuildConfig
metadata:
  name: my-build-config
spec:
  runPolicy: Serial
  source:
      git:
        ref: master
        uri: https://github.com/mmumshad/simple-webapp-docker
      type: Git
  strategy:
      dockerStrategy:
      type: Docker
  output:
    to:
      kind: ImageStreamTag
      name: 'simple-webapp-docker:latest'
  triggers:
    - type: ConfigChange

Build Trigger :


 

This is done using webhook 

GITLAB
Does not allow local deployment 
	


Deployments


In kuberntes the smallest unit which can be deployed is called POD which is essentially one or more docker containers they depended on each other grouped together 

As of now think 
A Pod is single instance of docker 

To scale up application we need replication of POD

Deployment controller -  help in managing application lifecycle management( such as rollback, stop, pause etc)

Container >> POD >> Replication Controller >> Deployment controller >>


Loadbalancer -> when we have the new version of software running and client are still using the older version and we want to shift the client from older version to upgraded new version of software then we make use of routers and loadbalancer 


 


 
	
To check ip address 

 
Services and routing

Scaling Application
Enable to fetch new instance each time 
  


Storage.
Docker last for very short period of time. They are called when required to process data and destroyed when finished. The same thing happen to data the data is destroyed along with containers.
 



Example Voter Application 

 


Templated and catalog
 
 

Sample yml for deployement : run >> oc export service db
Why we use custom templates ?
Aim is to package all the component to get a fully working application.

Customer templates get the following data: 
Db
Build config
Image Stream
Deployment  
Services 
Routes


oc login -u app-developer-2
  	
Error
 
For this you must create a namespace and provide the name.
 









What is DevOps Engineer ?
 

https://www.youtube.com/watch?v=CnqjHRCZEt0

 

