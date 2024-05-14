### Build docker image
docker build -t nginx .

### Run docker container
docker run --rm -it -p 8080:80 nginx

--rm tells docker to remove the container once its stopped, and the -it is used to attach interactive TTY, the -p 8080:80 is used to map the port 80 from the container to our computer port 8080, so if we access localhost:8080 it means we are accessing the container.ip:80