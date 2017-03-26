# GSoC Application 
The application for Stand-alone Reactome server in a Docker image. It describes idea of project, regarding which components are to be included and proposed timeline for the project. Doc version available at [Google Drive](https://drive.google.com/open?id=1uvufmjdR8ci0z2getY3nLT3vZxZrWUAqBOCMV_VWwe8) (First Draft Completed)

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
