FROM jenkins/jenkins:lts-centos

USER root

# 安装docker
RUN yum install -y wget yum-utils device-mapper-persistent-data lvm2 && \
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo && \
    dnf install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm && \
    yum update -y && \
    yum install -y docker-ce

# 安装docker-compose
WORKDIR /usr/local/bin
RUN wget https://raw.githubusercontent.com/topsale/resources/master/docker/docker-compose
RUN chmod +x docker-compose
COPY daemon.json /etc/docker/daemon.json


# 安装 Maven
WORKDIR /usr/local
RUN wget https://mirror.bit.edu.cn/apache/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz
RUN tar -zxvf apache-maven-3.5.4-bin.tar.gz -C /usr/local/
RUN mv /usr/local/apache-maven-3.5.4/conf/settings.xml /usr/local/apache-maven-3.5.4/conf/settings.xml.bak
RUN rm apache-maven-3.5.4-bin.tar.gz
COPY settings.xml /usr/local/apache-maven-3.5.4/conf

# 配置环境变量
ENV MAVEN_HOME /usr/local/apache-maven-3.5.4
ENV PATH $PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin

WORKDIR /

EXPOSE 8080
EXPOSE 50000