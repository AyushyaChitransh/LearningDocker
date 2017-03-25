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
3. Fireworks and FireworksJS
4. Other Java Applications

These components are yet to be discussed with the mentor. Furthermore we will dicuss about which are the other java applications that are to be included and when will be their source code available.

#### Wordpress Website
It requires a LAMP stack. And presently the site is configured to run on apache2 > 2.4, using php5 and php5-mysql. Docker will require a fresh installation and when installed in an ubuntu image, all components will be easily installed using `RUN apt-get` in dockerfile. After installing all components of LAMP server, it can be configured by running the bash script. 
#### Tasks
1. Preparing a Base Image or using a pre-existing image.
2. Writing the Dockerfile for making image for LAMP server. 
3. Writing the bash script to configure the server created in the image.

Regarding the base image, we have two choices. Either going with traditional Ubuntu image, or using a Alpine distro. 
Alpine Linux is a Linux distribution built around musl libc and BusyBox. It is much smaller than most distribution base images (~5MB), and thus leads to much lighter images. _This is yet to be discussed with the mentor._

These will be primary tasks in this phase. The end product will be a container with a configured LAMP server. Official github repository of tomcat provides with two options, using a readymade tomcat image or using a dockerfile to create own image. I shall be using dockerfile since it will award me a higher degree of freedom to configure every aspect of server during creation.
***

Phase 2 (2 weeks)
---
Docker images are made layer by layer. Using the image made in previous layer, other components can be added in subsequent layers to make a new image. 
Reactome uses php5-mysql as RDBMS. There already exists a database which needs to be added and configured in the docker image. When docker will be created for the first time, a bash file will create the database which will be updated from the centralized database.
#### Task
1. Install and configure php5-mysql.
2. Create database using a script. Update this database to match the live database(Reactome's centralized database).
***

Phase 3 (4 weeks)
---
Reactome contains two JAVA based components for visulation of dataset analysis viz. Fireworks and FireworksJS.
Fireworks is a java application that provides hierarchical visualisation of dataset analysis results in the context of the Reactome  pathway structure. Similarly FireworksJs is an exporter of the diagram viewer to a Javascript API.

Reactome has a component named Pathway analysis service (AnalysisTools) which provides an API for pathway over-representation and expression analysis as well as species comparison tool. Reactome has other java applications such as 
1. InteractorExporter
2. Graph-importer
3. Graph-core
4. Search-indexer
5. Data-content
6. CuratorTool
7. SBMLExporter
8. Search-core
9. AnalysisTools
10. Data-export 
11. Pathway-Exchange
12. Models2Pathways

#### Task
1. Analyze all components and determine their prerequisites and dependencies.
2. Adding all prerequisites and dependencies followed by the components.

***

Phase 4 (2 weeks)
---
After making all components of Reactome available in the docker image, the installation procedure of those components needs to be tested. 
After succesfull testing image will be deployed on the standard image repository such as dockerhub or quay.io (_as suggested by mentor_) that can be pulled and run on any Docker-capable workstation. A user guide will also be added for easier Installation and operation of the Docker.


#### Task
1. Formal Testing
2. Deploy the image to be available for download.
3. Provide user-guide
***    

Personal information
---

__Name:__ Ayushya Chitransh
__Email:__ ayushyachitransh@gmail.com
__Github:__ ayushyachitransh
__Education:__ Final year undergrad pursuing B.Tech in Computer Science and Engineering. 
__About Ayushya:__  I fell in love with C and it is my most obvious choice for all basic problems. However I do love to code and explore C#, Java and Python. I don't have any commitments this summer and I will be able to dedicate most of my time to my project.
