#Container for Kafka - Spark streaming - Cassandra
#IMPORTANT: If you wish to share folder between your host and this container, make sure the UID for user guest is the same as your UID
#Check https://github.com/Yannael/brufence/blob/master/docker/streaming/README.md for details
FROM ubuntu:22.04

#Needed for avoiding interactive prompt during tzdata installation (triggered by openssh-server - https://techoverflow.net/2019/05/18/how-to-fix-configuring-tzdata-interactive-input-when-building-docker-images/)
ENV DEBIAN_FRONTEND=noninteractive

# Install basic tools
RUN apt-get update
RUN apt-get install -y wget nano git unzip curl gcc openssh-server

#Install Java. Java 8 preferable. Java 11 gives warnings about reflexive classes with PySpark
RUN apt-get install -y openjdk-8-jdk

#Create guest user. IMPORTANT: Change here UID 1000 to your host UID if you plan to share folders.
RUN useradd -ms /bin/bash guest -u 1000
RUN echo "guest:guest" | chpasswd

USER guest

ENV HOME /home/guest
WORKDIR $HOME

#Install Anaconda Python distribution
RUN wget https://repo.anaconda.com/archive/Anaconda3-2023.03-Linux-x86_64.sh
RUN bash Anaconda3-2023.03-Linux-x86_64.sh -b

ENV PATH $HOME/anaconda3/bin:$PATH

#Install Spark (Spark 3.3.2 - 23/03/2023, prebuilt for Hadoop 3.3 or higher)
RUN wget https://dlcdn.apache.org/spark/spark-3.3.2/spark-3.3.2-bin-hadoop3.tgz
RUN tar xvzf spark-3.3.2-bin-hadoop3.tgz \
	&& mv spark-3.3.2-bin-hadoop3 spark \
	&& rm spark-3.3.2-bin-hadoop3.tgz

#Install Kafka
RUN wget https://downloads.apache.org/kafka/3.4.0/kafka_2.13-3.4.0.tgz
RUN tar xvzf kafka_2.13-3.4.0.tgz \
	&& mv kafka_2.13-3.4.0 kafka \
	&& rm kafka_2.13-3.4.0.tgz

# Setting up required environment variables
ENV SPARK_HOME $HOME/spark
ENV KAFKA_HOME $HOME/kafka
ENV PATH $HOME/spark/bin:$HOME/spark/sbin:$HOME/kafka/bin:$PATH
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/pyspark.zip:$SPARK_HOME/python/lib/py4j-0.10.9.2-src.zip:$PYTHONPATH

#Install Kafka Python module
RUN pip install --upgrade pip
RUN pip install kafka-python geopandas rtree

RUN echo "alias notebook=\"jupyter notebook --ip='*' --NotebookApp.iopub_data_rate_limit=2147483647 --no-browser \" " >> /home/guest/.bashrc

USER root

#Startup (start Zookeeper, Kafka servers)
#ADD kafka_startup_script.sh /usr/bin/kafka_startup_script.sh
#RUN chmod a+x /usr/bin/kafka_startup_script.sh
