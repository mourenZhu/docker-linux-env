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

# 安装编译OpenWrt官方实例相关工具
RUN apt install -y build-essential clang flex bison g++ gawk \
gcc-multilib g++-multilib gettext git libncurses5-dev libssl-dev \
python3-setuptools rsync swig unzip zlib1g-dev file wget

# 安装当前镜像对当前OpenWrt编译所需要库
RUN apt install -y libelf-dev locales

# 设置LOCALE
RUN locale-gen en_US.UTF-8

# 修改root密码
RUN echo 'root:pw' | chpasswd

# 添加自定义用户
RUN adduser buildbot \
    && echo 'buildbot:pw' | chpasswd

# 安装ssh
RUN apt install -y openssh-server
RUN mkdir -p /var/run/sshd


# 开放22端口
EXPOSE 22
#设置自启动命令
CMD ["/usr/sbin/sshd", "-D"]