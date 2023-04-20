# Basic Commands

1. docker container run --publish 80:80 nginx

    This command will run a new container of image nginx and will expose the port 80 of the container to the port 80 of host. The -f option creates a firewall rule in the container, mapping a container port to a port on the Docker host to the outside world.

2. docker container run --publish 80:80 nginx --detach nginx

    Run the container in the background.

3. docker container ls

    List the running containers

4. docker container ls -a

    List all containers, even the stale ones.

5. docker container logs (container_name)

    Displays the logs of the container_name specified.

6. docker container top (container_name)

    Lists the processes running inside the container.

7. docker container rm (container_id1) (container_id2) (container_id3) ...

    Delete/Remove the stale container, throws an error for the running container. With option -f it will force delete.

8. docker container inspect (container_name)

    Returns a json object, containing all the data on how the container was started with the configuration.

9. docker container stats

    Returns realtime stats of the running containers

10. docker container run -it

    Runs the container and provides an interactive session to work with. There is usually a default command provided by the image(configured during image creation) that gets overwritten while using -it.

    Ex: docker container run -it --name temp nginx bash (On running the command bash as a command would be triggered and we will get a prompt.)

11. docker container start -ai (container_name)

    Starts an existing container in the interactive mode.

12. docker container exec -it (container_name) (command_name)

    This runs a command(command_name) in a running container. If a container is already running it will run a process/command inside that.

13. docker container inspect --format '{{NetworkSettings.IPAddress}}' container_name

    To inspect json data with a specif property.

14. docker network ls

    Shows all the networks that have been created

15. docker network inspect (network_name)

    Shows the configuration of the network_name.

16. docker network create (network_name)

    Creates a network of a driver type bridge(default).

17. docker container run -d --name (container_name) --network (network_name)

    Initiates a container in the specified network.

18. docker network connect (network_name) (container_id)

    To assign the container to the network.

19. docker network disconnect (network_name) (container_id)

    Dynamically removes a NIC from a container on a specific virtual network. Essentially, removing the container from the network. 


