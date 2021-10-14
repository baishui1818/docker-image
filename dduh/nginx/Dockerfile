# This My first Dockerfile
# Version 1.0
# Author: 2020-08-24

#Base image使用的基本镜像
FROM library/centos:7.5.1804

#MAINTAINER 创建人
MAINTAINER kasim

#RUN安装依赖包
RUN yum install -y wget gcc gcc-c++ make openssl-devel svn nfs-utils crontabs net-tools 

#下载源码包
RUN wget https://ftp.pcre.org/pub/pcre/pcre-8.37.tar.gz \
	&& wget http://nginx.org/download/nginx-1.14.0.tar.gz \
		&& tar -zxf pcre-8.37.tar.gz -C /usr/local/src \
			&& tar -zxf nginx-1.14.0.tar.gz -C /usr/local/src

#RUN wget http://update2.agent.tencentyun.com/update/linux_stargate_installer \
#	   && chmod +x linux_stargate_installer\
#		&&./linux_stargate_installer

#WORKDIR 进入工作目录
WORKDIR /usr/local/src/nginx-1.14.0

#初始化安装组件
RUN ./configure --prefix=/usr/local/nginx \
         --user=root --group=root \
                 --with-http_ssl_module \
                        --with-http_realip_module \
                                --with-http_stub_status_module \
                                        --with-pcre=/usr/local/src/pcre-8.37 \
                                                && make && make install
#进入安装目录
WORKDIR /usr/local/nginx/conf
#书写配置文件
RUN echo "#user  www www;" > /usr/local/nginx/conf/nginx.conf \
&& echo "worker_processes  8;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "pid /var/run/nginx.pid;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "worker_rlimit_nofile 65535;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "events {" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    worker_connections  1024;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "}" >> /usr/local/nginx/conf/nginx.conf \
&& echo "http {" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    include       mime.types;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    default_type  application/octet-stream;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    sendfile        on;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    server_names_hash_bucket_size 128;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    client_header_buffer_size 2048m;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    large_client_header_buffers 4 64k;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    client_max_body_size 8m;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    autoindex on;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    tcp_nopush on;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    tcp_nodelay on;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    keepalive_timeout  120;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    fastcgi_connect_timeout 300;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    fastcgi_send_timeout 300;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    fastcgi_read_timeout 300;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    fastcgi_buffer_size 64k;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    fastcgi_buffers 4 64k;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    fastcgi_busy_buffers_size 128k;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    fastcgi_temp_file_write_size 128k;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    gzip  on;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    gzip_min_length 1k;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    gzip_buffers 4 16k;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    gzip_http_version 1.0;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    gzip_comp_level 2;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    gzip_types text/plain application/x-javascript text/css application/xml;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    gzip_vary on;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    log_format main '\$remote_addr -  \"\$http_x_forwarded_for\" \$remote_user [\$time_local] \"\$request\" '"  >> /usr/local/nginx/conf/nginx.conf \
&& echo "                    '\$status \$body_bytes_sent \"\$http_referer\" '"  >> /usr/local/nginx/conf/nginx.conf \
&& echo "                    '\"\$http_user_agent\" ';" >> /usr/local/nginx/conf/nginx.conf \
&& echo "      access_log logs/access.log main;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    server {" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        listen       80 default_server;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "#        listen       [::]:80 default_server;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        server_name  _;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        root         /data/wwwroot;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        include /usr/local/nginx/conf/conf.d/*.conf;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        location / {" >> /usr/local/nginx/conf/nginx.conf \
&& echo "              root /data/wwwroot;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "              index  index.html index.htm;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "              set_real_ip_from 0.0.0.0/0;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "              real_ip_header X-Forwarded-For;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        }" >> /usr/local/nginx/conf/nginx.conf \
&& echo "      access_log /data/log/access.log main;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "      error_log /data/log/error.log;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        error_page 404 /404.html;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "            location = /40x.html {" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        }" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        error_page 500 502 503 504 /50x.html;" >> /usr/local/nginx/conf/nginx.conf \
&& echo "            location = /50x.html {" >> /usr/local/nginx/conf/nginx.conf \
&& echo "        }" >> /usr/local/nginx/conf/nginx.conf \
&& echo "    }" >> /usr/local/nginx/conf/nginx.conf \
&& echo "}" >> /usr/local/nginx/conf/nginx.conf \
#守护进程
&& echo "daemon off;" >> /usr/local/nginx/conf/nginx.conf
#创建网站目录和logs
RUN mkdir /data/wwwroot -p && mkdir /data/log && mkdir /test
#创建站点首页
RUN echo "Hello Word" >/data/wwwroot/index.html
#删除源码包
RUN rm -rf /usr/local/src/nginx-1.14.0 \
	&& rm -rf /usr/local/src/pcre-8.37
#配置时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& echo 'Asia/Shanghai' >/etc/timezone
#配置变量
ENV PATH /usr/local/nginx/sbin:$PATH
#声明端口
EXPOSE 80
#启动运行
CMD ["nginx"]
