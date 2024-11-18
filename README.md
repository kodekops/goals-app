# Docker Networking

## WWW Connection

By default,docker containers can communicate with the web(www),so no need to
do any extra configuration.

## Docker to Host Connection

Docker containers can communicate with the host machine by using the following
host address.

```bash
host.docker.internal
```

## Docker container to Docker container Connection

Docker container can communicate with each other with the ip address of the
docker container.We can get the IP address of the docker container by inspecting
the docker container,For this we need to run the following command.

```bash
docker container inspect contaner_name
```

So each time we need to run the above command to get the ip address of the
source container to communicate with the destination container.

So to avoid this we can create a user defined network and attach the containers
to the user defined network,so that the containers can communicate with each
with the container name.

So First of all,we need to create a docker network using the following command.

```bash
docker network create goals_app_net
```

We can view all the available networks by using the following command.

```bash
docker network ls
```

After that, we need to run the docker container for mongo db with in the created
network using the following command.

```bash
docker container run -d --name mongodb --network goals_app_net -p 27017:27017 mongo
```

After that we can use the container name to communicate with this container from
another container with in the same network.

For this we can run the following command to run the nodejs application container

```bash
docker container run -d --name goals_app --network goals_app_net -p 3000:3000 goals_app
```
