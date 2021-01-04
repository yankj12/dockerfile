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
# 自 redis 6.0.0 之后，编译 redis 需要支持 C11 特性，C11 特性在 4.9 中被引入。Centos7 默认 gcc 版本为 4.8.5，所以需要升级gcc版本。
#############
# https://download.redis.io/releases/redis-5.0.10.tar.gz
# http://download.redis.io/releases/redis-6.0.9.tar.gz

RUN yum install -y gcc gcc-c++ make openssl openssl-devel wget
#	&& yum -y install centos-release-scl \
#	&& yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils
#RUN scl enable devtoolset-9 bash \
#	&& echo "source /opt/rh/devtoolset-9/enable" >>/etc/profile
#	# 安装redis6需要上面三行命令以及scl

RUN	cd /home \
	&& wget -O redis.tar.gz "https://download.redis.io/releases/redis-5.0.10.tar.gz" \
	&& tar -xvf redis.tar.gz \
	&& cd /home/redis-5.0.10 \
	&& make && make PREFIX=/usr/local/redis install \
	&& mkdir -p /usr/local/redis/conf/ \
	&& cp /home/redis-5.0.10/redis.conf  /usr/local/redis/conf/ \
	&& sed -i  '68s/127.0.0.1/0.0.0.0/' /usr/local/redis/conf/redis.conf \
	&& sed -i  '87s/protected-mode yes/protected-mode no/' /usr/local/redis/conf/redis.conf	
ENTRYPOINT /usr/local/redis/bin/redis-server /usr/local/redis/conf/redis.conf