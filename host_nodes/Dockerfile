FROM ubuntu:latest
LABEL maintainer="Spencer Shepard"
LABEL description="A simple starting point for host containers with SSH enabled and ready to go."
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
COPY ../keys/id_rsa.pub /root/.ssh/authorized_keys
CMD ["/usr/sbin/sshd", "-D"]