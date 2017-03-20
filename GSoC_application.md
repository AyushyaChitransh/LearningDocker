# Project Idea			

Title: Stand-alone Reactome server in a Docker image
    
Introduction: Reactome is an online bioinformatics database of human biology described in molecular terms. It is an on-line encyclopedia of core human pathways. The goal of this project is to produce a Docker image that contains  everything that is needed for a user to run Reactome on their own workstation. Provisions will be made to update the database with the latest centralized database.

Expected results: A Docker image that can be pulled from an image repository such as dockerhub or quay.io which contains the latest Reactome data and software, and can be run on any Docker-capable workstation. A process by which such docker images could be automatically built as a part of the Reactome data-release cycle would also be a goal. 

Current Status: Currently there is no image. It has to be made from a base image as suitable for the project.

Steps:
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

Collect components of reactome: Reactome has following components: a WordPress site, a MySQL database, and Java applications.

Requirements: 
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
	
	
    Components
fireworks
diagram
Solr
RESTful


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



		Week 2 (June 7 to june 13)		

Install tomcat apache
Installing tomcat needs some research about customizations.
Configuring tomcat for ubuntu 16.04
Scripting the automation procedure

Automation of installation procedure needs testing.
Fresh installation may work correctly, but restarting
failed installlation procedure may be tricky.
=========================================================



		Week 3 (June 14 to june 20)		


=========================================================



		Week 4 (June 21 to june 27)		

Scripting Automation Procedure for complete setup.
Creating a docker using ubuntu 16.04 image.
=========================================================



		Week 5 (June 28 to july 4)		

Deploying docker image to be available for downloaded.
Optimizing dockerfile to run on slow networks also.
=========================================================



		Week 6 (july 5 to july 11)		

Testing docker image.
Installing and testing other api and services.
=========================================================



		Week 7 (july 12 to july 18)		

Making entire setup accessible on single machine.
Testing interdependency among different components.
=========================================================



		Week 8 (july 19 to july 25)		

Seting up automatic updation of code from reactome github.
Customizing updation process.
=========================================================



		Week 9 (july 26 to aug 1)		

Allowing data shairing between users.
Customizing to be able to access local database as well as
online database.
=========================================================



		Week 10 (aug 2 to aug 8)		

Debugging and testing for any errors or fails.
Documentation of code for developers.
Documentation for User.
=========================================================



		Week 10 (aug 9 to aug 15)		

Review of functions from potential users.
Debugging and updating documentation.
=========================================================



		Week 11 (aug 16 to aug 21)		

=========================================================



			About Me			

Name: Ayushya Chitransh
Email: ayushyachitransh@gmail.com

Background: Ayushya is a final year undergraduate pursuing
his B.Tech in computer Science.

Programming Experience: C is the chouce for all basic problems
however C, Java and Python are other languages of choice.

Programming Strenghts: C is my favourite language
Work:
=========================================================
