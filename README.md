# dockerfiles
Collection of dockerfiles

## fastai docker setup

### streaminterrupt/fastai (My awesome docker)
github repo for building [paperspace/fastai](https://github.com/Edutech-ARM/dockerfiles/tree/master/fastai)

`nvidia-docker run --rm --init -it --name container1 -p 8888:8888 streaminterrupt/fastai:cuda9-cudnn7-ubuntu16.04`

### Paperspace/fastai 
github repo for building [paperspace/fastai](https://github.com/Paperspace/fastai-docker)
```
nvidia-docker run --rm --init -it --name container1 -p 8888:8888 -w="/notebooks" paperspace/fastai:cuda9_pytorch0.3.0
OR
nvidia-docker run --rm --init -it --name container1 -d -p 8888:8888 -w="/notebooks" paperspace/fastai:cuda9_pytorch0.3.0
```
if you run docker using -d option then for getting jupyter link run `docker logs <container-name>` so in this case `docker logs container1`
