FROM ubuntu:latest
LABEL maintainer="Spencer Shepard"
LABEL description="This is will create the Ansible control node image with ssh and some useful tools."
RUN apt-get update
RUN apt-get install -y python3 python3-pip
RUN apt-get install -y vim nano curl wget git net-tools iputils-ping dnsutils
RUN apt-get install -y openssh-server openssh-client
RUN apt-get install -y sudo
RUN pip3 install ansible

#enable ssh login with password
RUN echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config
RUN mkdir -p /run/sshd

#copy ssh key to root user
COPY ../keys/id_rsa /root/.ssh/id_rsa
RUN sudo chmod 600 /root/.ssh/id_rsa

#create ansible user
ARG password=ansible
RUN useradd -m -s /bin/bash ansible
RUN echo "ansible:$password" | chpasswd
RUN usermod -aG sudo ansible
RUN echo "ansible ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
USER ansible
WORKDIR /home/ansible

#copy ssh key to ansible user
COPY ../keys/id_rsa /home/ansible/.ssh/id_rsa
RUN sudo chown -R ansible:ansible /home/ansible/.ssh
RUN sudo chmod 600 /home/ansible/.ssh/id_rsa

#we'll need to add any env vars to the ansible user's .profile if we want them available between sessions
RUN echo "ANSIBLE_HOST_KEY_CHECKING=False; export ANSIBLE_HOST_KEY_CHECKING" >> /home/ansible/.profile

CMD ["sudo", "/usr/sbin/sshd", "-D"]
