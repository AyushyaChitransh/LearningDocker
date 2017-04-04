# Project Idea			

## Title:
Stand-alone Reactome server in a Docker image
    
##### Introduction: 
Reactome is an online bioinformatics database of human biology described in molecular terms. It is an on-line encyclopedia of core human pathways. The goal of this project is to produce a Docker image that contains everything that an end-user needs to run Reactome on his/her own workstation. Provisions will also be made to update the database in the image with the latest centralized database of Reactome.



##### Expected results: 
A Docker image that can be pulled from an image repository such as dockerhub or quay.io which contains the latest Reactome data and software, and can be run on any Docker-capable workstation. A process by which such docker images could be automatically built as a part of the Reactome data-release cycle would also be a goal.

##### Current Status:
Currently there is no docker image. It has to be made from a base image as suitable for the project. Reactome runs a wordpress site also which requires LAMP server. An official image of LAMP stack is not available but we can start with an official docker image of tomcat which is based on openjdk:7-jre-alpine, i.e., using alpine as base image.

##### Steps:
1. List out the components of reactome.
2. Requirements/dependencies of each component.
3. Creating containers for each underlying service.
4. Composing a docker using those containers.
5. Making the image available on image repository such as dockerhub.
6. Providing user guide to run different services on docker.

##### Components:
1. Wordpress Website
2. Pathway Browser
3. Fireworks and Fireworks JS
4. Other Java Application

#### Services:
For the components discussed above there are some prerequisites and other services that are essential and these will be deployed in separate containers and combined in the docker. 

1. MySql
2. Apache2
3. Tomcat
4. Solr
5. Neo4J
6. Perl
7. Java

***

## Phase 1 (May 30 to June 26)

There are two approaches of making a docker. Either use a dockerfile to make a single container or make multiple containers and combine then together using docker compose. Containers are ephemeral. To make sure data is preserved between runs, we can use volumes, which will be shared and persisted between containers. This is easily done with second approach ,i.e, using compose. Compose is a tool for defining and running multi-container Docker applications. It offers following [features](https://docs.docker.com/compose/overview/#features): 

1. Multiple isolated environments on a single host.
2. Preserve volume data when containers are created.
3. Recreate only those containers that have their states changed.
 
The components will be deployed in their own containers. This phase requires the individual containers to be built for different services required by the component. Different component will be combined together using docker compose.
The services mentioned above will be run in their isolated containers and components will be built using them. Furthermore , there are some JAVA applications and some perl scripts which need to be made available to the Reactome. Perl scripts will be made available in a container in which perl will be installed. Similarly, JAVA applications will be made available by using their Jar/WAR files.

### Wordpress Website

It requires a LAMP stack. And presently the site is configured to run on apache2 > 2.4, using php5 and php5-mysql. The following services are required by wordpress website:

1. Apache2
2. Tomcat
3. Php 5
4. WP-CLI
5. mysql 
 

Containers for Tomcat, apache2, php5 and WP-CLI will be made in this phase. Every service will run in a separate container.  While the official docker images are available for tomcat, apache and mysql, it will be better to use one’s own dockerfile since it will allow a higher degree of freedom to configure every aspect of server during creation. All services can be installed using their respective dockerfile and further configuration can be made by running a bash script.

__SSL__: Tomcat dockerfile will also provide self signed SSL certificate for secure access to the site that it is running.

Installing Wordpress Plugins manually by using admin pages will be a overhead so the required wordpress plugins will be installed by the dockerfile itself. This can be achieved by using WP-CLI.
WP-CLI is a set of command-line tools for managing WordPress plugins without using a web browser. It is as simple as the following code/snippet:

```
$ wp plugin install custom_plugin --activate
```

One can checkout the documentation [here](https://wp-cli.org/commands/plugin/install/).  WP-CLI will be used to install and update plugins via dockerfile. 

Regarding the base image, we have two choices. Either going with traditional Debian image, or using a Alpine distro. Alpine Linux is a Linux distribution built around musl libc and BusyBox. It is much smaller than most distribution base images (~5MB), and thus leads to much lighter images. Using alpine as the base image for different containers will keep the Docker image size to minimal. While a debian based image may increase docker size but will run smoothly because of the fact that original reactome server runs on debian. This will be decided by experimentation when the coding part begins.

These will be primary tasks in this phase. The end product will be a collection of containers configured as per required services.

#### Tasks

1.  Preparing independent and isolated containers for different services, by using a dockerfile or using a pre-existing official image of that service if available.
2.  Preparing a base Image using dockerfile for the components whose official docker image is not available.
3.  Writing the bash script to configure the services created for components in the image.
4.  Compose a docker out of the containers of components.

---
## Phase 2 (June 30 to July 24)
**Database**: Reactome uses php5-mysql as RDBMS. There already exists a database which needs to be added and configured in the docker image. When docker will be created for the first time, a bash file will replicate the database in the volumes of docker image. The script will update the database in the image with master database on reactome server if newer database is available on the central server.

**Neo4j**: Reactome uses neo4j. It is a graph database management system. Its official docker image for every version is available and desired version can be included in docker-compose. 

**Perl**: Also one of the components in Reactome uses perl, so we will need to install perl. Official docker image of perl has its vulnerabilities. So we shall create our own image by installing only required modules. There are a number of perl modules required to be included and the necessary modules will be installed.

**Solr**: Solr is an open source enterprise search platform, written in Java. To use Solr, we need to create a "core" using script at start time, as an index for Reactome data. Core can be created in several ways, and we shall be using Docker-compose to create a Solr container with the index stored in a named data volume.

**Java**: Reactome contains two JAVA based components for visualization of dataset analysis which are Fireworks and Fireworks JS. Fireworks is a java application that provides hierarchical visualisation of dataset analysis results in the context of the Reactome pathway structure. Similarly Fireworks Js is an exporter of the diagram viewer to a Javascript API.
    The java applications will be made available in a single container by specifying their Jar files. Reactome has a component named Pathway analysis service (Analysis Tools) which provides an API for pathway over-representation and expression analysis as well as species comparison tool. 
Reactome has other java applications such as: 
1. Interactor Exporter 
2. Graph-importer 
3. Graph-core
4. Search-core
5. Search-indexer 
6. Data-content 
7. Curator Tool 
8. SBML Exporter 
9. Analysis Tools 
10. Data-export 
11. Pathway-Exchange 
12. Models 2 Pathways

### Tasks

1. Install and configure Neo4j, perl and Solr.
2. Script installation procedure for php5-Mysq
3. Replicate the Reactome’s live database to a local database. And provide
4. functionality to update the local database with the live database (Reactome’s centralized database).
5. Analyze all components and determine their prerequisites and dependencies.
6. Adding all prerequisites and dependencies followed by the components.

---

## Phase 3 (August 15 to August 21)

After making all components of Reactome available in the docker image, the installation procedure of those components needs to be tested. After successful testing image will be deployed on the standard image repository such as dockerhub or quay.io (as suggested by mentor) that can be pulled and run on any Docker-capable workstation. A user guide will also be added for easier Installation and operation of the Docker.

**August 22 to August 29** : This week is set aside as a buffer to negate any time lost/lag in work.

### Tasks

1. Formal Testing.
2. Deploy the image to be available for download.
3. Provide documentation and user-guide.

---

### Personal information

**Name**: Ayushya Chitransh

**Email**: ayushyachitransh@gmail.com 

**Github**: ayushyachitransh 

**Background**: I am a final year undergraduate pursuing B.Tech in Computer Science and Engineering. I don't have any commitments this summer and I will be able to dedicate most of my time to my project.

#### Programming interests and strengths

**What are your languages of choice?**
I have been programming for quite a long time, and it was in last 3 years that I was introduced to the open source world. During these three years while pursuing my bachelor’s degree in computer science, I have worked on a diverse variety of projects, which includes:
**Two desktop applications** for conducting a two day technical quiz in the college:

1. [RiseOfUltron](https://github.com/AyushyaChitransh/Medicrum)
2. [Rise Of Ultron- Finale](https://github.com/AyushyaChitransh/Technical-Quiz-2)
 
**Two web applications**, both for industrial purposes
1. [Floor - Automation](https://github.com/AyushyaChitransh/MGT-automation): To automate the manual process of tracking and scheduling various operations in the company.
2. [Medicrum](https://github.com/AyushyaChitransh/Medicrum): An online platform for bringing together retailers, buyers and suppliers of medicines.

My final year project, [Abstractive Text Summarization](https://github.com/AnupKumarGupta/AbstractiveTextSummarizer), is to provide a summary of a larger piece of text, implemented using abstractive summarization technique. All of the projects mentioned above are available on  Github.

#### Any prior experience with open source development?

Being a supporter of open source, I like to share my experience in ubuntu and solve problems of users at askubuntu community. I also contributed to docker.io with a merged pull request  for an improvement in the documentation of docker.io.

#### Your interest and background in biology or bioinformatics.

While looking for organizations I can contribute to, I was specifically searching for organizations in biological domain. This project aims at creating a docker image for biologists which will enable them to have the entire functionalities of reactome on their machine and help them in their work. These researchers have the knowledge and I want to provide them with the tools they need. I feel proud to be able to assist these researchers in their work. With this project I hope to make their work easier and in the process, learn from the experienced open source developers.

#### Any prior exposure to biology or bioinformatics?
I have no exposure to bioinformatics and limited knowledge about biology. But this project does not require an intensive knowledge about bioinformatics, thus I believe that it will not impair my ability to work on this project.

#### What can you bring to the team?
Having done an internship in industrial environment and being a part of technical community in our college, I bring along a sense of teamwork, coordination, ability to work under pressures and deadlines. 
