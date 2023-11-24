# Docker tips

# Docker images/container commands
sudo docker images # docker image listing
sudo docker rmi -f images_names # deleting images with force
sudo docker ps -a # docker container listing (all)

# Docker image building (based on Dockerfile)
sudo docker biuld -t image_name:tag .

# Run container with host volume mounting
sudo docker run --name container_name -v host_directory:/container_direktory -it image_name /bin/bash
