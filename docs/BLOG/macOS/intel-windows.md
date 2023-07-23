# Intel Mac Windows 10 安装

## 安装条件

首先确认自己的电脑是否可以安装 Windows，这需要满足以下两个条件（摘自 [Apple Support | Install Windows 10 on your Mac with Boot Camp Assistant](https://support.apple.com/en-us/HT201468)）：

- Mac 的 CPU 是 Intel 的 CPU
- 不需要 U 盘进行安装的 Mac：
    - MacBook introduced in 2015 or later
    - MacBook Air introduced in 2017 or later
    - MacBook Pro introduced in 2015 or later
    - iMac introduced in 2015 or later
    - iMac Pro (all models)
    - Mac Pro introduced in late 2013 or later

如果你的 Mac 为 ARM CPU，那么打开 Boot Camp Assistant 会出现不支持的说明。

## 准备所需工具

其次需要下载 Windows 10 的系统镜像文件：[Microsoft | Download Windows 10 Disc Image (ISO File)](https://www.microsoft.com/en-us/software-download/windows10ISO)；如果你在 Windows 安装完成好后还需要科学上网，最好在执行下面的操作之前下载好科学上网的工具。然后将系统镜像文件和你需要的工具放到一个 U 盘里面。

## 将 macOS 升级至最新并格式化

接下来我们需要格式化 Mac，使得其有足够多的空间来为 Windows 提供磁盘。在这一步之前，请确定你已经不再使用这台 Mac 并通过 U 盘拷贝了其中你还需要用到的文件。参考 [Apple Support | Use Disk Utility to erase an Intel-based Mac](https://support.apple.com/en-us/HT208496)：

- 如果你的 macOS 为 Monterey 或更高（包括 Ventura），查看 [Apple Support | Erase your Mac and reset it to factory settings](https://support.apple.com/en-us/HT212749)
- 否则查看 [Apple Support | Use Disk Utility to erase an Intel-based Mac](https://support.apple.com/en-us/HT208496)

由于第一种方法相比第二种方法简单许多，我推荐先在设置中将 macOS 升级到最新。

## 安装 Windows

接下来就可以使用 Boot Camp Assistant 安装 Windows 了。

- 打开 U 盘，将 Windows 10 的镜像文件拷贝到 macOS，并将 U 盘弹出
- 打开 Boot Camp Assistant，会自动识别 Windows 10 镜像文件
- 一路点击下一步

## 在 Windows 中做设置

- 打开转换助理做触控板设置
- 通过修改注册表调整触控板自然滚动（参考 [CSDN | 更改 MacBook Pro 中 Win10 的触摸板双指滑动的方向（改为自然滚动）](https://blog.csdn.net/booksyhay/article/details/80712601)）
    - 在设置中查看触控板的设备实例路径
    - 打开运行 regedit 并回车
    - 找到 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\HID\VID_???\Device Parameters 下面的 FlipFlopWheel，将其值由 0 改为 1

## 删除 Windows

如果你之后不需要使用 Windows 了，可以重启打开 macOS，通过 Boot Camp Assistant 删除 Windows 分区。
