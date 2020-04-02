# Example strictly confined snap that uses docker 

This is an example snap that uses the docker snap to provide the docker executables and the docker snap. 

### Building

You will need to build it locally, as it is not published in the store. First install snapcraft:

```
$ snap install snapcraft
```

(note it will ask you to acknowledge you are installing a classic snap with the `--classic` option)

Then clone this repo and just run:

```
$ snapcraft
```

### Installing and using

After the snap is built, install it with `--dangerous`:

```
$ snap install --dangerous docker-snap-usage-example_0.1_amd64.snap
```

Trying to run it without doing anything else will fail because we need to connect interfaces manually:

```
$ docker-snap-usage-example.docker 
the docker-executables content interface must be connected first!
please run "snap connect docker-snap-usage-example:docker-executables docker:docker-executables"
$ snap connect docker-snap-usage-example:docker-executables docker:docker-executables
$ docker-snap-usage-example.docker run hello-world
the docker socket interface must be connected first!
please run "snap connect docker-snap-usage-example:docker docker:docker-daemon"
$ snap connect docker-snap-usage-example:docker docker:docker-daemon
$ docker-snap-usage-example.docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```