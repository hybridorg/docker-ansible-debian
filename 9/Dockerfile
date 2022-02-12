FROM debian:stretch
LABEL maintainer="Tinashe Chikomo <tinashe@chikomo.net>"

ENV container docker
ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive

ENV pip_packages "ansible pymysql cryptography yamllint ansible-lint"

# Install dependencies.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    apt-utils sudo make gcc openssl zlib1g-dev wget ca-certificates libffi-dev libssl-dev

RUN wget -q https://www.python.org/ftp/python/3.8.2/Python-3.8.2.tgz -O /tmp/Python-3.8.2.tgz && \
    tar -xzf /tmp/Python-3.8.2.tgz -C /tmp && \
    cd /tmp/Python-3.8.2 && \
    ./configure && \
    make && make install \
    && rm -rf /tmp/Python-3.8*

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       sudo systemd systemd-sysv python3-apt \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean

# Upgrade pip to latest version
RUN python3.8 -m pip install --upgrade pip

# Install Ansible via pip.
RUN python3.8 -m pip install $pip_packages

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible
ADD https://raw.githubusercontent.com/hybridadmin/misc-scripts/master/linux/ansible/hosts /etc/ansible/hosts
ADD https://raw.githubusercontent.com/hybridadmin/misc-scripts/master/linux/ansible/ansible.cfg etc/ansible/ansible.cfg

RUN rm -f /lib/systemd/system/multi-user.target.wants/* \
    /etc/systemd/system/*.wants/* \
    /lib/systemd/system/local-fs.target.wants/* \
    /lib/systemd/system/sockets.target.wants/*udev* \
    /lib/systemd/system/sockets.target.wants/*initctl* \
    /lib/systemd/system/sysinit.target.wants/systemd-tmpfiles-setup* \
    /lib/systemd/system/systemd-update-utmp*

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/lib/systemd/systemd"]
