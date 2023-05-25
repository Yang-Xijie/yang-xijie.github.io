# UOS 相关链接

## 官方

### 官网

- [统信软件技术有限公司 官网](https://www.uniontech.com)
- [统信UOS家庭版 官网](https://home.uniontech.com)
    - [帮助文档](https://home.uniontech.com/help/zh_CN/Home/)
    - [校园联盟](https://home.uniontech.com/campus/campus.html)
    - [U粉俱乐部](https://club.uniontech.com/#/index)
- [统信UOS生态社区 官网](https://www.chinauos.com)
    - [开发者专区 DTK](https://www.chinauos.com/developMode/dtk)
    - [开发者专区 统信UOS论坛](https://bbs.chinauos.com)
    - [资源中心 镜像下载](https://www.chinauos.com/resource/download-home) 包含桌面家庭版 桌面专业版 服务器版
- [统信开发者文档](https://docs.uniontech.com/zh/)

### 官方账号

- [Bilibili 统信UOS官方账号](https://space.bilibili.com/455091158)
- 微信公众号 统信UOS ID: UOS-EDU
- 微信公众号 统信软件 ID: uniontech_UOS

## Mac虚拟机使用

- [VMware Fusion](https://www.vmware.com/cn/products/fusion.html)
    - [Bilibili | Mac云课堂 - VMware Fusion个人版免费使用方法](https://www.bilibili.com/video/BV1jK41137UJ)
- [Parallels® Desktop 17 for Mac](https://www.parallels.cn)
    - [Mac虚拟机教学① 什么是虚拟机？为什么选择 Parallels](https://www.bilibili.com/video/BV1Zt41197Fd)
    - [Mac虚拟机教学② 手把手带你安装 Parallels 和 Windows 10](https://www.bilibili.com/video/BV1Zt41197FP)

## 开发

### DTK

[统信开发套件DTK Development ToolKit](https://www.chinauos.com/developMode/dtk)

终端命令 —— 搭建DTK开发环境

```sh
# 更新仓库索引
sudo apt update

# 安装基础的开发工具
sudo apt install g++ make cmake gdb

# 安装Qt及Qt Creator
sudo apt install qt5-default qtcreator qtbase5-examples

# 安装DTK开发库
sudo apt install libdtkwidget-dev libdtkgui-dev libdtkcore-dev
 
# 安装DTK工程模板
sudo apt install qtcreator-template-dtk
```
