FROM centos:7.4.1708

#author
MAINTAINER yankj12
ENV DEBIAN_FRONTEND noninteractive
RUN  mkdir -p /usr/local/mysql
ADD  mysql /usr/local/mysql

#WORKDIR /usr/local/mysql
RUN  groupadd mysql
RUN  useradd -g mysql mysql
RUN  cd /usr/local
RUN  chmod 775  /usr/local/mysql
RUN  chown -R mysql.mysql /usr/local/mysql
RUN  yum -y install libaio-devel
RUN  yum -y install numactl
ENTRYPOINT sh /usr/local/mysql/start.sh
