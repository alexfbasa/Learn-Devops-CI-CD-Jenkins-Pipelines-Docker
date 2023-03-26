FROM jenkins/jenkins:lts
USER root

RUN apt-get update
RUN apt-get install -y maven
RUN apt-get install -y net-tools

RUN apt-get install -y python3-pip
RUN mkdir -p /tmp/download && \
    curl -L  https://download.docker.com/linux/static/stable/x86_64/docker-18.03.1-ce.tgz > docker-18.03.1-ce.tgz && tar -xzf docker-18.03.1-ce.tgz -C /tmp/download && \
    rm -rf /tmp/download/docker/dockerd && \
    mv /tmp/download/docker/docker* /usr/local/bin/ && \
    rm -rf /tmp/download && \
    groupadd -g 998 docker && \
    gpasswd -a jenkins docker && \
    usermod -aG docker jenkins

# Install app dependencies
RUN pip install --upgrade pip
#RUN pip install ansible --upgrade
USER jenkins