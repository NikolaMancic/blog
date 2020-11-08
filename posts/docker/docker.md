# Understanding Docker & containerization

## __About Docker__

Docker is a tool that allows software to run in isolated containers on it's host system. It is a popular solution for running software in an easily reproducible fashion.

Learn more [here](https://www.docker.com/why-docker)

`BONUS`: Check out other containerization technologies such as `rkt` (Rocket) and `LXC` Linux Containers

`BONUS`: Read up on the predecessors to containers: `chroot` and BSD Jails

### __Installing Docker__

Docker is almost certainly available in the standard repository of almost any mainstream Linux distribution. Let's install it via:

``` sh
sudo apt install docker.io
```

`NOTE:` On Raspberry Pi OS, as well as other Debian based distributions, the package is called `docker.io` since there was an older (but unrelated) package called `docker` already. Make sure to check beforehand if you're following along on a different distribution.

Let's install `docker-compose`, too:

``` sh
sudo apt install docker-compose
```

`docker-compose` is used to startup multiple, pre-configured containers at once.

In order to manage the docker engine, images and containers we need to make sure that our user is part of the `docker` group. Check current group membership via:

``` sh
groups
```

The `groups` command prints all groups our current user is a member of. If the `docker` group is missing we can add it via:

``` sh
usermod -a -G docker pi
```

The format is `usermod -a -G <group> <user>`. `usermod`, as the name suggest, is a command that modifies user accounts. The `-G` flag specifies we want to make a group related change. The `-a` flag specifies we want to append a new group. `<group>` is the name of the group we want to append. `<user>` is the name of the user we want to append it to.


Once we add our user to the group we can check if we have permission to use docker via:

``` sh
docker ps
```
