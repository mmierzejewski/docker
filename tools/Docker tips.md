Docker tips
=====

### Docker images/container commands

```
sudo docker images -a                          # docker image listing
sudo docker rmi -f image_name1 image_name2     # deleting images with force
sudo docker ps -a                              # docker container listing (all)
sudo docker system prune -a                    # purging all anused or dangling images, containers, volumes, and networks

### Docker image building (based on Dockerfile)

```
sudo docker biuld -t image_name:tag . 
```

### Run container with host volume mounting

```
sudo docker run --name container_name -v host_directory:/container_direktory -it image_name /bin/bash
```

### Helples links
* https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes
* https://towardsdatascience.com/how-to-mount-a-directory-inside-a-docker-container-4cee379c298b
