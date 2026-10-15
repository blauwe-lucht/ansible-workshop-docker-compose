FROM rockylinux/rockylinux:9-ubi-init

ARG ANSIBLE_UID=1000

RUN dnf install -y openssh-server python3 hostname iproute procps-ng \
    && dnf clean all

RUN useradd --uid "${ANSIBLE_UID}" ansible \
    && echo "ansible:ansible" | chpasswd \
    && install -d -o ansible -g ansible -m 0700 /home/ansible/.ssh

COPY authorized-key.service /etc/systemd/system/authorized-key.service
RUN systemctl enable sshd authorized-key
