# 以最新的Ubuntu镜像为模板
FROM ubuntu:22.04

# 设定环境变量，防止交互卡住
ENV DEBIAN_FRONTEND=noninteractive
ARG TZ=Asia/Shanghai

# 替换为你自己的源前，先装好 ca-certificates
RUN apt update && apt install -y ca-certificates

# 将本目录下的sources.list作为容器的一个文件
ADD sources.list /root/sources.list
# 使用国内Ubuntu源，更新快
RUN mv /etc/apt/sources.list  /etc/apt/sources.list_bak
RUN cp /root/sources.list  /etc/apt/sources.list

# 安装常用工具
RUN apt update && apt install -y vim git openssh-server

# 修改root密码
RUN echo 'root:123456' | chpasswd

# 添加自定义用户
RUN adduser zhumouren \
    && echo 'zhumouren:123456' | chpasswd

RUN usermod -aG sudo zhumouren

RUN mkdir -p /var/run/sshd


# 开放22端口
EXPOSE 22
#设置自启动命令
CMD ["/usr/sbin/sshd", "-D"]