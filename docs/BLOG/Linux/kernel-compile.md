# Linux 内核编译尝试

## 资源

- [Linux From Scratch](https://www.linuxfromscratch.org/lfs/)
    - [Linux From Scratch - online en](https://www.linuxfromscratch.org/lfs/view/stable/)
    - [Linux From Scratch - online zh](https://bf.mengyan1223.wang/lfs/zh_CN/11.1/index.html)
- [QEMU](https://www.qemu.org/docs/master/)
    - [QEMU doc | Linux boot specific](https://www.qemu.org/docs/master/system/invocation.html?highlight=bzimage#hxtool-8)
    - [BLOG | Booting a Custom Linux Kernel in QEMU and Debugging It With GDB](http://nickdesaulniers.github.io/blog/2018/10/24/booting-a-custom-linux-kernel-in-qemu-and-debugging-it-with-gdb/)
    - [BLOG | How to build and boot a custom disk image in qemu](https://blog.w2h.co/qemu_linux.html)
    - [What is KVM?](https://www.redhat.com/en/topics/virtualization/what-is-KVM)

## 尝试

```sh
# 在<https://www.kernel.org>找到最新的稳定版链接，复制
# 使用wget下载.tar包
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.17.2.tar.xz
# 解压
tar xvf linux-5.17.2.tar.xz
# 进入之后退出生成默认配置.config
(apt install libncurses-dev &&) make menuconfig
# 编译
(apt install libssl-dev libelf-dev &&) make
# 安装模块
make modules_install
# 安装在本机
make install
```

遇到的问题

```
make[1]: *** No rule to make target 'debian/canonical-certs.pem', needed by 'certs/x509_certificate_list'.  Stop.
```

参考<https://askubuntu.com/questions/1329538/compiling-the-kernel-5-11-11> 

```
scripts/config --disable SYSTEM_TRUSTED_KEYS
scripts/config --disable SYSTEM_REVOCATION_KEYS
```

## References

- [Bilibili | 迷途小书童的Note - linux内核编译](https://www.bilibili.com/video/BV1bV411C7x2)
