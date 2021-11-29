# 14848 Project option 1

Big data processing toolbox

Video Demo : https://youtu.be/BQV_w6BtvsM

Terminal Application Code Walkthrough : https://youtu.be/CVh0AsArjtI

jupyter notebook walkthrough : https://youtu.be/PO-w1V65Ebk

Docker images Used :

https://hub.docker.com/r/kish7/webtermapp

https://hub.docker.com/r/kish7/jupyter

https://hub.docker.com/r/kish7/sparkweb

https://hub.docker.com/r/kish7/hadoopui



## Installation
The Project contains 4 components deployed independently controlled by a web-based terminal application.

* Apache Hadoop
             
* Apache Spark
                  
* Jupyter Notebook
          
* Sonarqube

* Web-UI-based terminal application (Optional)

 

Use docker pull to pull all the required docker images in the cloud shell.

```bash
docker pull kish7/jupyter
docker pull kish7/sparkweb
docker pull kish7/hadoopui
docker pull kish7/jupyternote
docker pull kish7/webtermapp
```

Tag and push the docker images to GCP container registry
```bash
docker tag kish7/jupyter gcr.io/project_ID/kish7/jupyter
docker push gcr.io/project_ID/kish7/jupyter
```

```bash
docker tag kish7/sparkweb gcr.io/project_ID/kish7/sparkweb
docker push gcr.io/project_ID/kish7/sparkweb
```

```bash
docker tag kish7/hadoopui gcr.io/project_ID/kish7/hadoopui
docker push gcr.io/project_ID/kish7/hadoopui
```

```bash
docker tag kish7/jupyternote gcr.io/project_ID/kish7/jupyternote
docker push gcr.io/project_ID/kish7/jupyternote
```

```bash
docker tag kish7/webtermapp gcr.io/project_ID/kish7/webtermapp
docker push gcr.io/project_ID/kish7/webtermapp
```

## Deployment in GKE


Deploying Hadoop
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143803097-1b682d20-2e71-4bec-8b19-afa21c05d812.png">


Hadoop Service and Ingress
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143803054-5bf7551d-90e2-48d6-a665-29155fb0673b.png">


Hadoop UI 
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143803008-0208c5ef-15ac-485f-9d7b-4f841b28e300.png">



Deploying the Spark master and Spark worker Nodes

The Image used is based out of bitnami/spark

The environment variables need to be set for the master and the worker nodes appropriately

ENV Variables for master node

    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
      
ENV Variables for worker node

      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no

Selecting the docker image and setting the environment variables for spark Master 
<img width="1433" alt="image" src="https://user-images.githubusercontent.com/22275506/143795804-ec33c342-95e6-40e0-b80b-56701bd0ed14.png">

Deployed successfully
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143798497-b0f8565a-ab3e-4e17-aa5b-c481cb6a1904.png">

Spark service and Ingress
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143798564-70867327-c747-42aa-b733-9c12984aad73.png">



Spark dashboard
![spark _Dashboard](https://user-images.githubusercontent.com/22275506/143810802-86cc4af9-12d8-40bc-b339-6a70ff8b6d8c.JPG)





Deploying the worker node and setting the environment variables to point to the Master node
<img width="1433" alt="image" src="https://user-images.githubusercontent.com/22275506/143796042-1cafff96-2672-4c56-b9a9-d00b534cd1cc.png">

Deploying the Jupyter Notebook Docker image

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143800538-dd385487-d5d2-4d93-bf30-34200547f9ff.png">

Jupyter notebook Service and Ingress
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143800514-134e47a8-662c-4b6e-880b-7a610ac89266.png">


Jupyter notebook UI
Build a docker image with preconfigured password as 'kish' since token is needed to set the password everytime the container restarts.
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143800275-355dfa83-67c3-463d-99b6-d56004d1a253.png">

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143800447-54ae72ea-eccb-4cd7-97a2-435ebd48cd88.png">

Deploying Sonarqube
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143801723-819a9ab5-69da-41d5-a234-70075d9cbf22.png">


Sonar service and Ingress
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143801699-ac2b69df-b6fc-46d9-93c5-a94008ce4f2d.png">


Sonar UI
<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143801659-da0445c0-af8e-4e4f-b7f3-eaba0f7eb93d.png">

Deploying the terminal application 

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143810952-748fd0ae-378e-46e8-b06a-6dfb7b36749b.png">

Service and Ingress for terminal application 

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143810986-2ec75836-4a3c-4f3a-b2cb-367573dc1850.png">

Webterminal application UI

<img width="1440" alt="image" src="https://user-images.githubusercontent.com/22275506/143811017-e425bcd6-bbc8-4e18-a8a7-a077daeb52c3.png">





