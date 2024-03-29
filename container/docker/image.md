# What is an image?

A Docker image is a lightweight, stand-alone, and executable package that contains everything needed to run a piece of software, including the code, dependencies, libraries, and configuration files. It is essentially a snapshot of a container at a particular point in time.

## Storage drivers

Docker uses storage drivers to store image layers and to store data in the writable layer of container. The container's writable layer does not persist after the container is delete, but is suitable fro string ephemeral data that is generated at runtime.

## Image Layer

A docker image is built up from a series of layers. Each layer represents an instruction in the image's Dockerfile. Each layer except the very last one is a read-only. Commands in the docker file that modify the filesystem create a layer. Each layer is only a set of differences from the layer before it.

When a container is created a new writable layer on top of the underlying layers is added. this layer is often called the "container layer". All changes made to the running container such as writing new files, modifying existing files and deleting files are written to the thin writable layer.

![image_layer](/asset/images/docker/image_layer.png)

A storage driver handles the details about the ay these layers interact with each other. It also manages the contents of the storage layers including the thin writable layer. Each storage driver handles the implementation differently but all drivers use stackable image layer and the copy on write (CoW) strategy.
Copy on write is copying the files before making any changes. i.e. when a file needs to modified by a dockerfile command or in the writable layer, the file needs to be modified is first copied to the current layer and the modifications are done to that file. Making it more performant for read but at the same time degrading write performance for data intensive services like database.
