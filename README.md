#### Fork of https://github.com/jessfraz/dockerfiles

This fork only includes the instructions and dockerfile to run chromium inside docker on MacOS

### Setup

1. Install XQuartz: https://www.xquartz.org/
2. Allow network connections in XQuartz preferences (security tab)
3. Build dockerfile

  ```bash
    sudo docker build -t "quartzedchromium:dockerfile" .
  ```

4. Add/customize seccomp profile: https://raw.githubusercontent.com/jfrazelle/dotfiles/master/etc/docker/seccomp/chrome.json

### Run

1. Add host IP for auth:

  ```bash
    xhost + $(ifconfig en1 | grep inet | awk '$1=="inet" {print $2}')
  ```

2. Run XQuartz

  ```bash
  open -a XQuartz
  ```

3. Run container

  ```bash
  sudo docker run -e DISPLAY=[YOUR_IP]:0 -v /tmp/.X11-unix:/tmp/.X11-unix --privileged --security-opt seccomp=~/chrome.json quartzedchromium:dockerfile"
  ```
