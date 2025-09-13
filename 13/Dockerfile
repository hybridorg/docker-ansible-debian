FROM debian:trixie
LABEL maintainer="Tinashe Chikomo <tinashe@chikomo.net>"

ENV container=docker

ENV DEBIAN_FRONTEND=noninteractive

ENV pip_packages="ansible pymysql cryptography yamllint ansible-lint"

# Install dependencies.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       sudo systemd systemd-sysv \
       build-essential wget libffi-dev libssl-dev procps \
       python3-pip python3-apt \
       iproute2 curl \
    && pip3 install --break-system-packages uv \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean \
    && echo 'export PATH="$PATH:/root/.venv/bin"' >> /root/.bashrc

WORKDIR /root

# Install Ansible via pip. - source /root/.bashrc &&
RUN pip3 install --break-system-packages $pip_packages
#uv venv &&  uv pip install $pip_packages

COPY initctl_faker .
RUN chmod +x initctl_faker && rm -fr /sbin/initctl && ln -s /initctl_faker /sbin/initctl

# Install Ansible inventory file.
RUN mkdir -p /etc/ansible \
    && echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts

# Make sure systemd doesn't start agettys on tty[1-6].
RUN rm -f /lib/systemd/system/multi-user.target.wants/getty.target

VOLUME ["/sys/fs/cgroup"]
CMD ["/lib/systemd/systemd"]
