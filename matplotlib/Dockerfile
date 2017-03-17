#Download base image ubuntu 16.04
FROM ubuntu:16.04
 
# Update Software repository
RUN apt-get update
RUN apt-get install python-matplotlib -y
RUN apt-get install python-tk

#Copy an existing python script to home of container
#for displaying graphs
COPY graph.py /home/root/graph.py

#as soon as container starts, this graph will be shown
CMD python /home/root/graph.py
