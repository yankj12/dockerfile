FROM centos:7

#############
# 配置cento代理及yum源
#############
ENV MY_PROXY_URL="http://10.1.249.61:3128"
ENV HTTP_PROXY=$MY_PROXY_URL \
    HTTPS_PROXY=$MY_PROXY_URL \
    FTP_PROXY=$MY_PROXY_URL \
    http_proxy=$MY_PROXY_URL \
    https_proxy=$MY_PROXY_URL \
    ftp_proxy=$MY_PROXY_URL

#COPY Centos-7.repo.qh /etc/yum.repos.d/
#RUN cd /etc/yum.repos.d/ \
#	&& mv CentOS-Base.repo CentOS-Base.repo.bak \
#	&& mv Centos-7.repo.qh CentOS-Base.repo \
#	&& yum clean all \
#	&& yum makecache

#############
# 构造redis
#############
RUN yum install -y gcc gcc-c++ make openssl openssl-devel wget
RUN cd /home \
	&& wget -O redis.tar.gz "http://download.redis.io/releases/redis-6.0.9.tar.gz" \
	&& tar -xvf redis.tar.gz \
	&& make && make PREFIX=/usr/local/redis install \
	&& mkdir -p /usr/local/redis/conf/ \
	&& cp /home/redis-4.0.9/redis.conf  /usr/local/redis/conf/ \
	&& sed -i  '68s/127.0.0.1/0.0.0.0/' /usr/local/redis/conf/redis.conf \
	&& sed -i  '87s/protected-mode yes/protected-mode no/' /usr/local/redis/conf/redis.conf	
ENTRYPOINT /usr/local/redis/bin/redis-server /usr/local/redis/conf/redis.conf