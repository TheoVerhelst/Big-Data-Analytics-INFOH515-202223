# INFO-H515 - Big Data Scalable Analytics
#### [Link to the Virtual University](https://uv.ulb.ac.be/course/view.php?id=106385)
#### *Théo Verhelst, Cedric Simar and Gianluca Bontempi* - [Machine Learning Group](http://mlg.ulb.ac.be)
#### *Material from Yann-Aël Leborgne, Jacopo De Stefani and Gianluca Bontempi*

# Exercise classes - Overview

This repository contains the material for the exercise classes of the ULB/VUB Big Data Analytics master course (second semester 2022-2023) - Advanced analytics part.

These hands-on sessions provide:

* **Session 1** : An introduction to Spark and its Machine Learning (ML) library. The case study for the first session is a churn prediction problem: How to predict which customers will quit a subscription to a given service? The session covers the basics for loading and formatting a dataset for training an ML algorithm using Spark ML library, and illustrates the use of different Spark ML algorithms and accuracy metrics to address the prediction problem.
* **Session 2**: Map/Reduce programming model for distributing machine learning algorithms, and their implementation in Spark. Sessions 2 covers linear regression (ordinary least squares and stochastic gradient descent). The algorithms are applied on an artificial dataset, and illustrate the numpy and Map/Reduce implementations for OLS and SGD.
* **Session 3**: An introduction to cloud computing on the Google Cloud Plateform (GCP), with instructions on how to set up a virtual machine to execute distributed code on the cloud. The exercises focus on feature selection strategies.
* **Session 4**: Streaming analytics with Recursive Least Squares (RLS) and model racing. The algorithms are implemented using Spark Streaming, on a data stream coming from a Kafka broker. The RLS approach is then compared with established ML approaches.
* **Session 5**: Map/Reduce implementation of a recommender system with alternating least squares (ALS), using as a case study a movie recommendation problem.


The material is available as a set of Jupyter notebooks.

# Clone this repository

From the command line, use

```
git clone https://github.com/TheoVerhelst/Big-Data-Analytics-INFOH515-202223
```

If using the course cluster, you will have to use SFTP to send this folder to the cluster.

# Environment setup

These notebooks rely on different technologies and frameworks for Big Data and machine learning (Spark, Kafka, Keras and Tensorflow). We summarize below different ways to have your environment set up.

## Local setup (Linux)

### Python

Install Anaconda Python (see https://www.anaconda.com/download/, choose the latest Linux distribution (Python 3.9 at the writing of these instructions).

Make sure the binaries are in your PATH. Anaconda installer proposes to add them at the end of the installation process. If you decline, you may later add

```
export ANACONDA_HOME=where_you_installed_anaconda
export PATH=$ANACONDA_HOME/bin:$PATH
```

to your `.bash_rc`.

### Spark

Download from https://spark.apache.org/downloads.html (Use version 3.3.2 (February 2023), prebuilt for Apache Hadoop 3.3). Untar and add executables to your PATH, as well as Python libraries to PYTHONPATH

```
export SPARK_HOME=where_you_untarred_spark
export PATH=$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH
export PYTHONPATH="$SPARK_HOME/python/lib/pyspark.zip:$SPARK_HOME/python/lib/py4j-0.10.4-src.zip"
```

### Kafka

Download from https://kafka.apache.org/downloads, and untar archive. Start with

```
export KAFKA_HOME=where_you_untarred_kafka
nohup $KAFKA_HOME/bin/zookeeper-server-start.sh $KAFKA_HOME/config/zookeeper.properties  > $HOME/zookeeper.log 2>&1 &
nohup $KAFKA_HOME/bin/kafka-server-start.sh $KAFKA_HOME/config/server.properties > $HOME/kafka.log 2>&1 &
```

### Keras and tensorflow

Install with `pip`

```
pip install tensorflow
pip install keras
```

### Notebook

The notebook is part of Anaconda. Start Jupyter notebook with

```
jupyter notebook
```

and open in the browser at `127.0.0.1:8888`


## Docker

In order to ease the setting-up of the environment, we also prepared a [Docker](https://www.docker.com/) container that provides a ready-to-use environment. See `docker` folder for installing Docker, downloading the course container, and get started with it.

Note that the [Dockerfile](https://github.com/TheoVerhelst/Big-Data-Analytics-INFOH515-202223/blob/main/Docker/Dockerfile) script essentially follows the steps for the 'local' installation.

## Check if your setup is working

After setting up your environment (either in a Docker or your own machine) you should be able to run the notebook and scripts in `Check_Setup`

### Spark - Test with Check_Setup notebook

* Open notebook from  `Check_Setup/Demo_RDD_local.ipynb`
* Run all cells

Follow instructions in `Check_Setup/Demo_RDD_local.ipynb` to have access to Spark UI.
