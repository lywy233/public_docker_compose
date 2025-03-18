# 个人code server服务器

# miniconda路径 /root/miniconda3


# wsl等x86上构建
## 如果qemu报错，可尝试重装qemu-user-static 或如下方式急活
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes