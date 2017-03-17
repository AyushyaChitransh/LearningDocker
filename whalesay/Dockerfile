FROM docker/whalesay:latest

#fortune emits wise sayings
RUN apt-get -y update && apt-get install -y fortunes

#default speaks
CMD /usr/games/fortune -a | cowsay
