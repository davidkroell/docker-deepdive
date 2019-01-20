# Questions

## General knowledge
1. Explain the three core principles of Docker.
1. Why is there no `/boot` directory in most Docker Images?
1. How are Docker containers isolated from each other?
1. How is the speed of the syscall translation increased?
1. How do you start a Docker container after the host gets rebootet?

## Practical use
1. You are running an Apache webserver in an Docker container. How would you insert your VirtualHost configuration?
1. How do you access an Apache webserver which runs in a Docker container? The webserver listens to port 8080.
We want to access it from port 8000.
    - Write down a `docker run` statement.
    - How do you limit the access to only `localhost`?
1. How would you configure a Laravel application without changing the `.env` file?
1. You would like to run a PHP app inside Docker. You install Apache and PHP this way:
    ```Dockerfile
    RUN apt-get update
    RUN apt-get install -y apache2
    RUN apt-get install -y php 
    RUN apt-get install -y libapache2-mod-php 
    ```
    - How and why could this Dockerfile be improved?
    - How would you start the Apache webserver when starting the container? Explain the pros and cons of the options below.
    ```Dockerfile
    ENTRYPOINT ["/usr/sbin/apache2"]
    RUN apache2
    CMD ["apache2"]
    ```

## Advanced knowledge
1. There are three processes running inside a Docker container.
    - Would you consider this as an ideal solution?
    - Does a Docker host see the threads running inside a container?
1. You are running five Docker hosts in Swarm mode.
    - How do they communicate between each other?
    - Is the data they exchange encrypted?
1. A Docker host sees the processes running inside the containers.
Why does a Docker container not see the processes running on the host?
1. How would you run a Docker container as root (UID 0)?
1. You are developing an application in an compiled language (assuming C or Go).
    - How would you decrease the image size?
    - How to decrease the image size further by building a statically linked binary?

## Advanced practial use
1. How would you limit a containers resources? Which resources can be limited?
1. You would like to build a webapplication which shows the containers and their state.
    - How would you access this data?
    - Would it be possible to run this application inside a Docker container?
1. You are deploying a Laravel application to Docker.
    - How do you ensure high availability?
    - How to enable load balancing between the Laravel instances?
    - Does a user detect a failure of one instance if he is currently signed-in into the application?
1. Where do you store logs (assuming you run Apache)?
1. Assuming you run a Docker host in an lab environment where every student has SSH access to the server for development purpose and everyone is in the `docker` group.
    - How do you ensure that the system files do not get compromised through a directory mount?
