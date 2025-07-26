FROM docker.io/golang:1.24
LABEL org.opencontainers.image.source = "https://github.com/mcsps/docker-images"
RUN apt-get -y install bc gcc libgl1-mesa-dev libwayland-dev libx11-dev libxkbcommon-dev xorg-dev xvfb
RUN go install github.com/fyne-io/fyne-cross@latest
RUN go install github.com/tcnksm/ghr@latest

#RUN adduser -u 1000 -D appuser
#USER appuser
#WORKDIR /home/appuser
#CMD tail -f /dev/null
