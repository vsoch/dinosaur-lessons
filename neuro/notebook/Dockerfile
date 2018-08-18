FROM jupyter/scipy-notebook

# docker build -t vanessa/dinolesson-cognitiveatlas .

LABEL maintainer @vsoch

USER root

RUN apt-get update && apt-get install -y git
RUN pip install cognitiveatlas

# Add local files
ADD . /home/joyvan/
