#LearningDocker

Image 1: nginx_image
As shown in [introduction-to-the-dockerfile-command](https://www.howtoforge.com/tutorial/how-to-create-docker-images-with-dockerfile/#introduction-to-the-dockerfile-command), the image created runs a nginx server which allows access to 
localhost://info.php
localhost://index.html
localhost

Various html pages served by the server are shared by the host system, and host may add files in the /webroot folderwhich will be served by the server running in container.

Image 2: matplotlib
It was designed to display a simple graph using matplotlib from python.
Currently, the container is able to run python scripts but graph is not shown due to display devices not being initialized for container.
