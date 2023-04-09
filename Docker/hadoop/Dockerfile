FROM ubuntu:latest


# 安装需要 JAVA 和 HADOOP 的文件信息
ARG JAVA_FILE=jdk-8u162-linux-x64.tar.gz
ARG JAVA_NAME=jdk1.8.0_162
ARG JAVA_DIR=/usr/lib/jvm/
ARG HADOOP_NAME=hadoop-3.1.3
ARG HADOOP_FILE=hadoop-3.1.3.tar.gz
ARG HADOOP_DIR=/usr/local/


# 添加 JAVA 安装包和 HADOOP 安装包 
ADD "build/${JAVA_FILE}" "${JAVA_DIR}"
ADD "build/${HADOOP_FILE}" "${HADOOP_DIR}"


# 配置环境变量信息
ENV JAVA_HOME "/usr/lib/jvm/java"
ENV HADOOP_HOME "/usr/local/hadoop"


# 更新添加相关程序以及生成 SSH key 以及配置基本的 JAVA 环境
RUN apt-get update -y && \
    apt-get install vim openssh-server -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    ssh-keygen -q -N "" -t rsa -f /root/.ssh/id_rsa && \
    cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys && \
    mv "${JAVA_DIR}${JAVA_NAME}" "${JAVA_HOME}" && \
    mv "${HADOOP_DIR}${HADOOP_NAME}" "${HADOOP_HOME}" && \
    echo '/etc/init.d/ssh start' >> ~/.bashrc && \
    echo 'export JAVA_HOME=${JAVA_HOME}' >> ~/.bashrc && \
    echo 'export JRE_HOME=${JAVA_HOME}/jre' >> ~/.bashrc && \
    echo 'export CLASSPATH=.:${JAVA_HOME}/lib:${JAVA_HOME}/jre/lib' >> ~/.bashrc && \
    echo 'export PATH=$PATH:$JAVA_HOME/bin' >> ~/.bashrc && \
    echo 'HADOOP_HOME=${HADOOP_HOME}' >> ~/.bashrc && \
    echo 'HADOOP_COMMON_HOME=${HADOOP_HOME}' >> ~/.bashrc && \
    echo 'HADOOP_HDFS_HOME=${HADOOP_HOME}' >> ~/.bashrc && \
    echo 'HADOOP_MAPRED_HOME=${HADOOP_HOME}' >> ~/.bashrc && \
    echo 'HADOOP_YARN_HOME=${HADOOP_HOME}' >> ~/.bashrc && \
    echo 'HADOOP_INSTALL=${HADOOP_HOME}' >> ~/.bashrc && \
    echo 'HADOOP_COMMON_LIB_NATIVE_DIR=${HADOOP_HOME}/lib/native' >> ~/.bashrc && \
    echo 'HADOOP_LIBEXEC_DIR=${HADOOP_HOME}/libexec' >> ~/.bashrc && \
    echo 'JAVA_LIBRARY_PATH=${HADOOP_HOME}/lib/native:$JAVA_LIBRARY_PATH' >> ~/.bashrc && \
    echo 'HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop' >> ~/.bashrc && \
    echo 'PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin' >> ~/.bashrc


# 添加配置文件到 hadoop
COPY build/etc/hadoop/* "${HADOOP_HOME}/etc/hadoop/"
ADD build/sbin/* "${HADOOP_HOME}/sbin/"
