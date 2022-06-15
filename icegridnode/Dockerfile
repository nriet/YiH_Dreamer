# Using the VNC image to run DataTransfer
# Version 1

FROM kevensen/centos-vnc

MAINTAINER nriet

WORKDIR /app

USER root

ADD ncl.zip ncl.zip
ADD ncl.z01 ncl.z01
ADD ncl.z02 ncl.z02
ADD YiH_Dreamer.zip YiH_Dreamer.zip
ADD YiH_Dreamer.z01 YiH_Dreamer.z01
ADD YiH_Dreamer.z02 YiH_Dreamer.z02
ADD YiH_Dreamer.z03 YiH_Dreamer.z03
ADD YiH_Dreamer.z04 YiH_Dreamer.z04
ADD YiH_Dreamer.z05 YiH_Dreamer.z05

RUN yum update -y && \
    yum install -y p7zip && \
    yum clean all && \
    7za x ncl.zip && \
    7za x YiH_Dreamer.zip && \
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
