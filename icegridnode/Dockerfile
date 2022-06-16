# Using the VNC image to run DataTransfer
# Version 1

FROM kevensen/centos-vnc

MAINTAINER nriet

WORKDIR /app

USER root

ADD ncl ncl
ADD draw draw
ADD icegridgui.jar icegridgui.jar
RUN yum install -y java-1.8.0-openjdk nss && \
	yum clean all && \
	rm -rf /var/cache/yum

RUN yum install -y https://zeroc.com/download/ice/3.7/el7/ice-repo-3.7.el7.noarch.rpm && \
	yum install -y icegrid && \
	yum clean all && \
	rm -rf /var/cache/yum

# 编译生成语言库
RUN localedef -c -f UTF-8 -i zh_CN zh_CN.utf8

# 设置语言默认值为中文，时区改为东八区
RUN echo 'LANG="zh_CN.UTF-8"' > /etc/locale.conf

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


ENV NCARG_ROOT /app/ncl
ENV YiH_Dreamer /app/draw
ENV PATH $PATH:$NCARG_ROOT/bin:$YiH_Dreamer
ENV LD_LIBRARY_PATH :$YiH_Dreamer/depend:$NCARG_ROOT/lib:$LD_LIBRARY_PATH

ENV LANG zh_CN.UTF-8
ENV LC_ALL zh_CN.UTF-8

RUN ldd /app/draw/YiH_Dreamer 

RUN /bin/echo "icegridnode --Ice.Config=/app/draw/ice/conf/icegridnode.conf" >> /home/1001/.vnc/xstartup

RUN /bin/echo "icegridadmin --Ice.Config=/app/draw/ice/conf/icegridnode.conf -e "application add /app/draw/ice/conf/application.xml"" >> /home/1001/.vnc/xstartup 

RUN /bin/echo "java -jar icegridgui.jar" >> /home/1001/.vnc/xstartup 
