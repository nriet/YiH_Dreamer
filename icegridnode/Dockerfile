# Using the VNC image to run DataTransfer
# Version 1

FROM kevensen/centos-vnc

MAINTAINER nriet

WORKDIR /app

USER root

ADD ncl*
ADD YiH_Dreamer*

RUN yum update -y && \
    yum install -y kde-l10n-Chinese && \
    yum reinstall -y glibc-common && \
    yum clean all && \
    unzip ncl.zip && \
    unzip YiH_Dreamer.zip && \
    rm -rf ncl*.z* && \
    rm -rf YiH_Dreamer*.z* && \
    rm -rf /var/cache/yum

# 编译生成语言库
RUN localedef -c -f UTF-8 -i zh_CN zh_CN.utf8

# 设置语言默认值为中文，时区改为东八区
RUN echo 'LANG="zh_CN.UTF-8"' > /etc/locale.conf

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ENV NCARG_ROOT /app/ncl
ENV PATH $PATH:$NCARG_ROOT/bin
ENV YiH_Dreamer /app/YiH_Dreamer
ENV LD_LIBRARY_PATH :$YiH_Dreamer/depend:$NCARG_ROOT/lib:$LD_LIBRARY_PATH

ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8


RUN /bin/echo "/app/YiH_Dreamer/YiH_Dreamer" >> /home/1001/.vnc/xstartup 
