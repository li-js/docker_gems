# Running graphical applications
If you are running on a Linux host, you can get code running inside the Docker container to display graphics using the host X server (this allows you to use OpenCV's imshow, for example). 
## On the host run:
```bash
sudo xhost +local:root
```
You can revoke these access permissions later with sudo xhost -local:root. 

## Start the docker by:
```bash
docker run --rm -it --init \
  --runtime=nvidia \
  -e "DISPLAY" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
  pytorch python3 -c "import tkinter; tkinter.Tk().mainloop()"
```
This will provide the container with your X11 socket for communication and your display ID.
Note that this is a quick-and-dirty (but INSECURE) way. For a more comprehensive guide on GUIs and Docker check out [here](http://wiki.ros.org/docker/Tutorials/GUI). Taken from [here](https://github.com/anibali/docker-pytorch)
