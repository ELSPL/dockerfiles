# dockerfiles
Collection of dockerfiles to ease multiple system setups

## fastai docker setup

### streaminterrupt/fastai (My awesome docker)
github repo for building [streaminterrupt/fastai](https://github.com/ELSPL/dockerfiles/tree/master/fastai)

`nvidia-docker run --rm --init -it --name container1 -p 8888:8888 streaminterrupt/fastai:cuda9-cudnn7-ubuntu16.04`

### Paperspace/fastai 
github repo for building [paperspace/fastai](https://github.com/Paperspace/fastai-docker)
```
nvidia-docker run --rm --init -it --name container1 -p 8888:8888 -w="/notebooks" paperspace/fastai:cuda9_pytorch0.3.0
OR
nvidia-docker run --rm --init -it --name container1 -d -p 8888:8888 -w="/notebooks" paperspace/fastai:cuda9_pytorch0.3.0
```
if you run docker using -d option then for getting jupyter link run `docker logs <container-name>` so in this case `docker logs container1`

---
## dl-lab docker

```
echo "LAB=~/docker_mount/NVIDIALabs/" >> ~/.bashrc
nvidia-docker run --rm --init -it --name container1 -p 5000:5000 -p 8888:8888 -v $LAB:/LAB -w="/LAB" streaminterrupt/dl-lab:base
OR
nvidia-docker run --rm --init -it --name container1 -p 5000:5000 -p 8888:8888 -v $LAB:/LAB -w="/LAB" streaminterrupt/dl-lab:v3
```

---
## ml-lab docker

```
cd ml-lab
// Configure below script and run
bash run_docker_jupyter.sh
```

---
## ros-lab docker

### streaminterrupt/ros-lab:v<x>
github repo for building [dockerfile](https://github.com/ELSPL/dockerfiles/tree/master/ROS-Melodic)

```
cd ROS-Melodic
// Configure below script and run
bash launch_docker.bash
```

### streaminterrupt/ros-lab:kinetic-v<x>
github repo for building [dockerfile](https://github.com/ELSPL/dockerfiles/tree/master/ROS-Kinetic)

```
cd ROS-Kinetic
// Configure below script and run
bash launch_docker.bash
```

---