# 使用 Ubuntu 22.04 作为基础镜像
FROM ubuntu:22.04

# 设置环境变量，避免交互式安装问题
ENV DEBIAN_FRONTEND=noninteractive

# 更新系统并安装必要的依赖
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    software-properties-common \
    && rm -rf /var/lib/apt/lists/*

# 下载并安装 Miniconda3
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh \
    && bash /tmp/miniconda.sh -b -p /root/miniconda3 \
    && rm /tmp/miniconda.sh

# 设置 Miniconda 环境变量
ENV PATH="/root/miniconda3/bin:$PATH"

# 确保 conda 运行正常，并更新 conda
RUN conda update -n base -c defaults conda -y

# 下载并安装 code-server
RUN curl -fsSL https://code-server.dev/install.sh | sh

RUN /root/miniconda3/bin/conda init bash \
    && echo ". /root/miniconda3/etc/profile.d/conda.sh" >> /root/.bashrc \
    && echo "conda activate base" >> /root/.bashrc
    
# 创建一个工作目录
WORKDIR /workspace

# 暴露 code-server 的默认端口
EXPOSE 8080

# 运行 code-server，并允许在容器外访问
# CMD ["code-server", "--bind-addr", "0.0.0.0:8080", "--auth", "none"]
CMD ["code-server"]