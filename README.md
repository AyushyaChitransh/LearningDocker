# GSoC Application for Stand-alone Reactome server in a Docker image
The application describing idea of project and proposed timeline with possible hurdles. (In Progress)

# LearningDocker

Image 1: nginx_image
As shown in [introduction-to-the-dockerfile-command](https://www.howtoforge.com/tutorial/how-to-create-docker-images-with-dockerfile/#introduction-to-the-dockerfile-command), the image created runs a nginx server which allows access to 
localhost://info.php
localhost://index.html
localhost
Various html pages served by the server are shared by the host system, and host may add files in the /webroot folderwhich will be served by the server running in container.

Image 2: matplotlib
It was designed to display a simple graph using matplotlib from python.
Currently, the container is able to run python scripts but graph is not shown due to display devices not being initialized for container.

Image 3: whalesay
A tutorial image which clears concepts of docker. The image installs a package 'Fortunes' which emits random sayings. The command is executed when image is run. It enables a saying to be displayed in terminal.
