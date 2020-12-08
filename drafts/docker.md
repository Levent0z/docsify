```
brew cask install docker
```
Run docker from Applications
Wait until Docker Desktop is "up and running"

# To setup your Docker:
#  Go to Preferences -> Resources -> Advanced and set Memory to 16GB, otherwise you may get premature termination with exit code 137 (out-of-memory)
#  Go to Preferences -> Resources -> File Sharing and add the folders /tmp and /secrets. See application.properties for more information.
#
# Note: In macOS Catalina, you can't add folders in root. Instead, use synthetic links:
#  $ sudo touch /etc/synthetic.conf
#  $ sudo # For the next line. The tab separator ("\t") is necessary.
#  $ printf "secrets\t$HOME/secrets\n" >/etc/synthetic.conf
#  $ exit



docker run -p 8088:8088 -p 15372:15372 -v /secrets:/secrets -v /tmp/runtime_files:/var/runtime_files -it --rm path/to/your_docker_image

To inspect the exit code, remove the "--rm" switch above and keep the container upon exit.