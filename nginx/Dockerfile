FROM nginx:1.15.8
MAINTAINER forfire "forfire@foxmail.com"
# 设置时区
COPY aliyun.list /etc/apt/
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone  \
    && cp /etc/apt/sources.list /etc/apt/bak.list && mv /etc/apt/aliyun.list /etc/apt/sources.list && apt-get update
RUN apt-get install -y \
        procps \
        vim \
        bash-completion \
        git
RUN usermod -u 1000 www-data && mkdir -p /data/logs/nginx && mkdir -p /data/wwwroot  && chown -R www-data:www-data /data
