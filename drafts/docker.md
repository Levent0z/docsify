```
brew cask install docker
```

Run docker from Applications
Wait until Docker Desktop is "up and running"

# To setup your Docker:

1. Go to Preferences -> Resources -> Advanced and set Memory to 16GB, otherwise you may get premature termination with exit code 137 (out-of-memory)
2. Go to Preferences -> Resources -> File Sharing and add the folders /tmp and /secrets. See application.properties for more information.

- Note: In macOS Catalina, you can't add folders in root. Instead, use synthetic links:
  ```bash
  sudo touch /etc/synthetic.conf
  sudo # For the next line. The tab separator ("\t") is necessary.
  printf "secrets\t$HOME/secrets\n" >/etc/synthetic.conf
  exit
  ```

```
docker run -p 8088:8088 -p 15372:15372 -v /secrets:/secrets -v /tmp/runtime_files:/var/runtime_files -it --rm path/to/your_docker_image
```

To inspect the exit code, remove the `--rm` switch above and keep the container upon exit.

# Getting Started:

```
$ docker run --name repo alpine/git clone https://github.com/docker/getting-started.git
$ cd getting-started
$ docker build -t docker101tutorial .
$ docker run -d -p 80:80 --name docker-tutorial docker101tutorial
$ docker tag docker101tutorial lozforce/docker101tutorial
$ docker push lozforce/docker101tutorial
```

Go to: http://localhost:80

`-d` : Detached mode (backgound)
`-t` : Tag
`-e` : Use previously exported environment variable

Use `docker scan` to run Snyk tests against images to find vulnerabilities and learn how to fix them

`docker ps` - List running containers

`docker stop CONTAINERID`

`docker rm CONTAINERID`

`docker rm -f CONTAINERID` - Stop before removing

`docker login -u USERNAME`

`docker tag NAME USERNAME/NAME`

`docker push USERNAME/NAME`

`docker images` - List images in local registry

# Test a docker image

```bash
docker login -u USERNAME IMAGEHOSTNAME
docker build -t IMAGENAME:latest .
docker run --rm -it IMAGENAME /bin/bash
```

## Example Docker File

```dockerfile
# Replace UPPERCASE values as needed
FROM CENTOSIMAGE
LABEL maintainer "emailadress@example.com"

RUN groupadd --system --gid 7447 USERNAME
RUN adduser --system --gid 7447 --uid 7447 --shell /bin/bash --home /home/USERNAME USERNAME

# set default location that is writable for the USERNAME
RUN mkdir -p /var/runtime_files && chown -R USERNAME:USERNAME /var/runtime_files
WORKDIR /home/USERNAME
ENV HOME=/home/USERNAME

# git is needed for npm install to work
RUN yum install git -y

COPY SOURCEFOLDER/ ${HOME}/DESTINATIONFOLDER

RUN chown -R USERNAME:USERNAME .
USER USERNAME

ENV HOME=/home/USERNAME
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:${PATH}

# RUN some command, OR
# ENTRYPOINT some command
```
