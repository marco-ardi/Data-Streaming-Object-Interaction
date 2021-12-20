[![CodeFactor](https://www.codefactor.io/repository/github/marco-ardi/data-streaming-object-interaction/badge)](https://www.codefactor.io/repository/github/marco-ardi/data-streaming-object-interaction)
# Data Streaming Object Interaction

# Important Note
This project has been improved and embedded in my Bachelor's Degree Project, [Hololens Object Interaction](https://github.com/marco-ardi/Hololens-Object-Interaction).
Check it out for a stronger and much more detailed solution!

## Overview
Project for my "Technologies for Advaced Programming" @ University of Catania.

![](https://github.com/marco-ardi/Data-Streaming-Object-Interaction/blob/main/Images/pipelinev4.png)


A Pipeline for real time object detection/interaction on data coming from a data source (Microsoft Hololens2) using ELK Stack.
A pair of Hololens2 sends, once per 4 seconds, a photo and a formatted log about eye gaze and hand position, via a TCP socket.
A socket server (python) receives these data, convert logs into 2D logs and stores on a Docker Volume.
Logstash reads from this volume and sends data to Apache Kafka, used for Data Collection.
Kafka sends a stream of data to Spark.
Spark (pySpark) applies [Detectron2](https://github.com/facebookresearch/detectron2) on the photo and checks whether there is a bounding box in the nearby of hand joints/eye gaze coordinates: if yes, that is an interaction and a list of interacted object is sent to ElasticSearch.
ElastiSearch is used for Data Indexing, these data are then used by Kibana for showing dashboard and insights.

## How to setup 
#### System requirement:
- Linux/MacOS/Windows WSL2
- Nvidia GPU (mandatory for using [Detectron2](https://github.com/facebookresearch/detectron2))
- Nvidia drivers/CUDA toolkit 11.1
- 🐋Docker/Docker-compose
- python 3.7 and openCV

#### Steps
- Clone this repository
- **Run** `docker-compose up --build`
- **Run** `python serverPy.py`
- **Run** `python stringConverter.Py`
