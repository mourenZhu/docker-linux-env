# 以最新的Ubuntu镜像为模板
FROM ubuntu:22.04

# 将本目录下的sources.list作为容器的一个文件
ADD sources.list /root/sources.list
# 使用国内Ubuntu源，更新快
RUN mv /etc/apt/sources.list  /etc/apt/sources.list_bak
RUN cp /root/sources.list  /etc/apt/sources.list

RUN apt update
# 安装常用工具
RUN apt install -y vim \
    && apt install -y bzip2 

# 安装ssh
RUN apt install -y openssh-server
RUN mkdir -p /var/run/sshd

# 配置ssh可以使用root登陆
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config

# RUN mkdir -p /var/run/sshd
# 修改root密码，便于远程登录
RUN echo 'root:pw' | chpasswd

# 复制配置文件到相应位置,并赋予脚本可执行权限
ADD run.sh /run.sh
RUN chmod 755 /run.sh

# 添加自定义用户
RUN adduser zmr \
    && echo 'zmr:zmr' | chpasswd

# 开放22端口
EXPOSE 22
#设置自启动命令
CMD ["/run.sh"]