# Debian Docker Images with ansible and systemd

> Debian Docker images to be used for testing ansible playbooks and roles.

## Supported tags and respective `Dockerfile` links

- [`latest`, `11` (*11/Dockerfile*)](https://github.com/hybridadmin/docker-debian-ansible/tree/main/11/Dockerfile)
- [`10` (*10/Dockerfile*)](https://github.com/hybridadmin/docker-debian-ansible/tree/main/10/Dockerfile)

## How to Build the image

1. Install docker
   * [Linux](https://docs.docker.com/engine/install/)
   * [Windows](https://docs.docker.com/docker-for-windows/install/)
2. Clone the repo `git clone https://github.com/hybridadmin/docker-debian-ansible.git`
3. `cd` into the directory
4. Run `docker build -t debian-ansible .`

## How to use this image

Pull the image using the following command:
```console
docker pull hybridadmin/debian-ansible:latest
```

Run a container using the image with the following command:
```console
docker run -d --name systemd-debian --privileged -v /sys/fs/cgroup:/sys/fs/cgroup:ro hybridadmin/debian-ansible:latest
```

Use Ansible inside the container:
```console
docker exec --tty [container_id] env TERM=xterm ansible --version
docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check
```

## Author

Created by Hybridadmin
