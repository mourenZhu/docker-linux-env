# 以最新的Ubuntu镜像为模板
FROM ubuntu:24.04

# 将本目录下的sources.list作为容器的一个文件
ADD sources.list /root/sources.list
# 使用国内Ubuntu源，更新快
RUN mv /etc/apt/sources.list  /etc/apt/sources.list_bak
RUN cp /root/sources.list  /etc/apt/sources.list

RUN apt update
# 安装常用工具
RUN apt install -y vim git

# 修改root密码
RUN echo 'root:123456' | chpasswd

# 添加自定义用户
RUN adduser zhumouren \
    && echo 'zhumouren:123456' | chpasswd

# 安装ssh
RUN apt install -y openssh-server
RUN mkdir -p /var/run/sshd


# 开放22端口
EXPOSE 22
#设置自启动命令
CMD ["/usr/sbin/sshd", "-D"]