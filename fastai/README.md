# Docker for fast.ai
![Docker Automated build](https://img.shields.io/docker/automated/jrottenberg/ffmpeg.svg)

![Docker Build Status](https://img.shields.io/docker/build/jrottenberg/ffmpeg.svg)
## Why Docker

- If you make a mistake while sorting out a mess of dependencies, you can just delete the Docker container and start from a fresh one; as opposed to trying to undo it on your operating system.
- Once you sort out a mess of dependencies, you'll never have to do it again. Even if you install a new operating system or move to a new computer, you can quickly recover your environment by downloading the corresponding Docker image or Dockerfile.
- You can have multiple ecosystems in form of containers that don't coexist otherwise on a machine.
- Also, no one else will have to go through that mess, because you can send them the Docker image or Dockerfile.

More information on basics, check out [this Docker tutorial for data science](https://towardsdatascience.com/how-docker-can-help-you-become-a-more-effective-data-scientist-7fc048ef91d5).
Also from usage point [refer this](https://tsaprailis.com/2017/10/10/Docker-for-data-science-part-1-building-jupyter-container/).


## Prerequisites

- A Machine with NVIDIA GPU.
  - If you don't, check out [Paperspace](http://forums.fast.ai/t/paperspace-setup-help/9290) or other GPU based cloud solutions such as Crestle, AWS or Azure.
- Docker CE [Installed](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/).
- NVIDIA Docker [Installed](https://github.com/NVIDIA/nvidia-docker).
- Manage Docker as a [Non-Root User](https://docs.docker.com/install/linux/linux-postinstall/).


## Host Setup

1\. Define your code and data paths by entering the following in a terminal:

```
CODE=~/docker_mount/code
DATA=~/docker_mount/data
```

2\. Clone the fast.ai repo onto your host machine by entering the following in a terminal:

```
git clone https://github.com/fastai/fastai.git $CODE/fastai
mkdir $DATA
wget http://files.fast.ai/data/dogscats.zip -O $DATA/dogscats.zip
unzip -q $DATA/dogscats.zip -d $DATA
```

3\. Spawn a docker container by entering the following in a terminal:

`nvidia-docker run --rm --init -it --name container1 -p 8888:8888 -v $CODE:/code -v $DATA:/data -w="/code/fastai" streaminterrupt/fastai:cuda9-cudnn7-ubuntu16.04`

4\. Start the Jupyter notebook server by entering the following alias into the container's terminal:

`jupyter_notebook_GPU_0_PORT_8888`

or

`j8`

5\. Authenticate your browser by opening the Jupyter notebook link that you see in the output (e.g. right click and press Open Link). It should look like this (your token value will be different): http://localhost:8888/?token=e73df183317f4d9283ab79fcd2b696220557db843036a1ff

6\. Open a Jupyter notebook in your browser and enjoy the fast.ai library.

---

To allow for faster access next time, enter the following into your host machine's terminal, only once:

`echo "alias fastai=\"nvidia-docker run --rm --init -it --name container1 -p 8888:8888 -v $CODE:/code -v $DATA:/data -w="/code/fastai" streaminterrupt/fastai:cuda9-cudnn7-ubuntu16.04\"" >> ~/.bashrc`

`source ~/.bashrc`

---

## Explanation

- `nvidia-docker run` can also be called as `docker run --runtime=nvidia` 

- `docker run`: Runs a container from a Docker image. A container is an instance of a Docker image, like an object is an instance of a class. A Dockerfile defines a Docker image, like a class definition defines a class.

- `--runtime=nvidia`: Gives the container access to the host's NVIDIA driver.

- `--init`: I don't really understand this option, but it's needed to make Jupyter notebooks run when a container is spawned. If you're curious, here are [the docs](https://docs.docker.com/engine/reference/run/#specify-an-init-process).

- `-it`: Creates a terminal for the container that the user on the host can interact with. To interact with terminal open another terminal and type `docker exec -it container1 bash`.

- `--name container1`: Name of the container to interact with it. Its not an image name. You can have multiple conatiners with different name of same image.

- `-rm`: Removes the container once it exits. Otherwise inactive containers pile up. To manually remove piled up container type `docker rm container1`

- `-p 8888:8888`: Binds the host's 8888 port to the container's 8888 port, allowing the host to access the container's Jupyter server through the host's Internet browser.

- `-v $CODE:/code` and `-v $DATA:/data`: Gives the container access to the host's `$CODE` and `$DATA` directories and calls them "/code" and "/data" from the container's perspective. **Note: any changes to the files, either made by the host or the container, will change those files from both the host's perspective and the container's perspective.**

- `-w="/code/fastai"`: Sets the working directory of the container, this is where jupyter notebook will open.

- `streaminterrupt/fastai:cuda9-cudnn7-ubuntu16.04`: Specifies the ID of the Docker image on [Docker Hub](https://hub.docker.com/). Docker Hub is like GitHub but for Docker images instead of code. The repository's name is "[streaminterrupt](https://hub.docker.com/r/streaminterrupt/fastai/)" and the Docker image's name is "[fastai](https://hub.docker.com/r/streaminterrupt/fastai/)". `docker run` will download the Docker image if it's not already on disk.

For more information, see [the Docker run reference](https://docs.docker.com/engine/reference/run/) and [the Docker run options list](https://docs.docker.com/engine/reference/commandline/run/).

You can [create a GitHub issue on this repo](https://github.com/Edutech-ARM/dockerfiles/issues/new) for any enhancements or bug reporting.

`jupyter_notebook_GPU_0_PORT_8888` is defined in the container's ~/.bashrc which spawns jupyter notebook:

```
alias jupyter_notebook_GPU_0_PORT_8888=\
      "ln -sf /data /code/fastai/courses/dl1/ && \
       source activate fastai && \
       CUDA_VISIBLE_DEVICES=0 jupyter notebook --port=8888 --allow-root"
```


## How to use the Docker image

If you've followed the setup and have set the aliases in bashrc then:

1. Enter `fastai` into a terminal.
2. Enter `j8` into the container's terminal that popped up as a result.

A Jupyter server will now be running in a fastai environment with all of fastai's dependencies.


## Build or Modify Docker Image

1. Clone this repository: `git clone https://github.com/Edutech-ARM/dockerfiles.git`
2. Change directory to fastai: `cd dockerfiles/fastai`
3. Modify the Dockerfile(if required) and Build: `docker build . -t streaminterrupt/fastai:<tag>`


## Docker Quick Reference

1. Working with Docker, [refer this](https://tsaprailis.com/2017/10/10/Docker-for-data-science-part-1-building-jupyter-container/).

2. Docker for Beginners, [refer this](https://medium.freecodecamp.org/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b) and [this](https://towardsdatascience.com/how-docker-can-help-you-become-a-more-effective-data-scientist-7fc048ef91d5).





