# Project Idea			

##### Title:
Stand-alone Reactome server in a Docker image
    
##### Introduction: 
Reactome is an online bioinformatics database of human biology described in molecular terms. It is an on-line encyclopedia of core human pathways. The goal of this project is to produce a Docker image that contains everything that an end-user needs to run Reactome on his/her own workstation. Provisions will be made to update the database in the image with the latest centralized database of Reactome.



##### Expected results: 
A Docker image that can be pulled from an image repository such as dockerhub or quay.io which contains the latest Reactome data and software, and can be run on any Docker-capable workstation. A process by which such docker images could be automatically built as a part of the Reactome data-release cycle would also be a goal. 

##### Current Status:
Currently there is no docker image. It has to be made from a base image as suitable for the project. A official image of LAMP stack is not available but we can start with an official docker image of tomcat which is based on `openjdk:7-jre-alpine`. This image is based on the popular Alpine Linux project,  Alpine Linux is much smaller than most distribution base images (~5MB), and thus leads to much slimmer images in general.
The base image needs to be discussed. Previously all components of reactome were deployed on ubuntu. Thus using ubuntu image as the base image will be ideal for the project.

##### Steps:
1) List out the components of reactome.
2) Requirements/dependencies of each component.
3) Installing components on local machine.
4) Testing Installations.
5) Creating Docker.
6) Making the image available on image repository such as dockerhub.
7) Providing user guide to run different services on docker.
***

Phase 1 (3 weeks)
===
Collect information regarding components of Reactome. 

### Components:
1. Wordpress Website
2. Pathway Browser
3. Fireworks
4. Diagram
5. RESTful APIs
6. Other Java Applications

These components are yet to be discussed with the mentor. Furthermore we will dicuss about which are the other java applications that are to be included and when will be their source code available.

#### 1.  Wordpress Website
It requires a LAMP stack. And presently the site is configured to run on apache2 > 2.4, using php5 and php5-mysql. Docker will require a fresh installation and when installed in an ubuntu image, all components will be easily installed using `run apt-get` in dockerfile. After installing all components of LAMP server, it can be configured by running the bash script. 
#### Tasks
1. Writing the Dockerfile for making image for LAMP server. 
2. Writing the bash script to configure the server created in the image.

These two will be primary tasks in this phase. The end product will be a container with a configured LAMP server. Official github repository of tomcat provides with two options, using a readymade tomcat image or using a dockerfile to create own image. I shall be using dockerfile since it will award me a higher degree of freedom to configure every aspect of server during creation.
***

Phase 2 (2 weeks)
---
Docker images are made layer by layer. Using the image made in previous layer, other components can be added on top of them.
Reactome contains two JAVA based components for visulation of dataset analysis.These are Fireworks and FireworksJS.
Fireworks is a java application that provides hierarchical visualisation of dataset analysis results in the context of the Reactome  pathway structure. Similarly FireworksJs is an exporter of the diagram viewer to a Javascript API.

solr service, MySQL
perl \
	curl \
	cpanminus \
	apache2 \
	php5 \
	php5-mysql \
	openjdk-7-jre-headless \
	openjdk-7-jdk\
	libexpat1 \
	libexpat1-dev \
	libgd-gd2-perl \
	libbio-perl-perl \
	cpanm -q \	HTTP::Tiny \	IO::String \	LWP::UserAgent \	MIME::Lite \	Net::OpenSSH \	XML::Simple \	Search::Tools \	Capture::Tiny \	WWW::SearchResult \	JSON \	PDF::API2 \	Log::Log4perl \	common::sense \	Email::Valid \	URI::Encode
	a2enmod \
    mime \
    include \
    autoindex \
    dir \
    cgi \
    alias \
    proxy \
    proxy_http \
    rewrite
    apache2 > 2.4
	apache-tomcat-7.0.50


WordPress Site
---
It requires a LAMP server which uses apache2 > 2.4 The server configuration files are already available but they need to be configured for specific system.
    
    Problem 1:
    Current system does not support java provided by oracle. The bug was reported in tomcat7 which was corrected later in tomcat8. Tomcat apache configuration needs to be updated.
php5 installation on local system failed due to the following reason
```
Package php5 is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
```
php5-mysql installation failed in the same manner.
The following packages were not installed because they had no installation candidate
1. php5
2. php5-mysql
3. openjdk-7-jre-headless
4. openjdk-7-jdk

Collecting Requirements for each component.
Install each component on local machine
Install tomcat apache
Installing tomcat needs some research about customizations.
Configuring tomcat for ubuntu 16.04
Scripting the automation procedure

Automation of installation procedure needs testing.
Fresh installation may work correctly, but restarting
failed installlation procedure may be tricky.
Looking up Directories to be included
Setup working directories with pages

Install Mysql
Setup database

Setting up directories for websites with database.


Phase 2	(2 weeks)
=========================================================			

Script installation procedure.
Start creation of docker image by installing all components.
=========================================================


		Phase 3 (3 weeks)			

Test the image by exeuting each component.
=========================================================


		Phase 4	(1 week)			

Document docker image and provide user guide.
=========================================================

