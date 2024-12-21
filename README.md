# Debian Docker Images with ansible and systemd

![Build](https://img.shields.io/github/actions/workflow/status/hybridadmin/docker-ansible-debian/build.yml) ![Docker Pulls](https://img.shields.io/docker/pulls/hybridadmin/ansible-debian)

> Debian Docker images to be used for testing ansible playbooks and roles.

## Quick reference

- Maintained by: [hybridadmin](https://github.com/hybridadmin)
- Where to get help: [The Docker Community Forums](https://forums.docker.com/), [Docker Community on Slack](https://dockr.ly/slack) or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)
- Where to file issues: [(issue tracker)](https://github.com/hybridadmin/docker-ansible-debian/issues) include the `docker` tag
- Supported Arch(s): [(more info)](https://github.com/docker-library/official-images#architectures-other-than-amd64) `amd64`

## Supported tags and respective `Dockerfile` links

- [`latest`, `12`](https://github.com/hybridadmin/docker-ansible-debian/tree/main/12/Dockerfile)
- [`11`](https://github.com/hybridadmin/docker-ansible-debian/tree/main/11/Dockerfile)
- [`10`](https://github.com/hybridadmin/docker-ansible-debian/tree/main/10/Dockerfile)
- [`9`](https://github.com/hybridadmin/docker-ansible-debian/tree/main/9/Dockerfile)

## How to Build the image

1. Install docker
   - [Linux](https://docs.docker.com/engine/install/)
   - [Windows](https://docs.docker.com/docker-for-windows/install/)
2. Clone the repo `git clone https://github.com/hybridadmin/docker-ansible-debian.git`
3. `cd` into the directory
4. Run `docker build -t ansible-debian .`

## How to use this image

Pull the image using the following command:

```console
docker pull hybridadmin/ansible-debian:latest
```

Run a container using the image with the following command:

```console
docker run -d --privileged -v /sys/fs/cgroup:/sys/fs/cgroup:rw --cgroupns=host hybridadmin/ansible-debian:latest
```

Use ansible inside the container:

```console
docker exec --tty [container_id] env TERM=xterm ansible --version
docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/playbook.yml --syntax-check
```

Connect to the container:

```console
docker exec -it [container_id] /bin/bash
```
