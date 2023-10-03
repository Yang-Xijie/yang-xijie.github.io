# Computer Graphics Notes

计算机图形学是所有东西的重中之重，其任务是将自然界的物体变为01存储到计算机，从计算机的01中将三维的物体显示在二维屏幕上。

## 学习资料

- 【持续更新】[Bilibili | 上帝视角看GPU](https://www.bilibili.com/video/BV1P44y1V7bu)
    - 可以先看这个了解GPU的工作原理，通过这个系列科普能把所有图形学的知识串起来；建议反复观看
- [Bilibili | GAMES101-现代计算机图形学入门 - 闫令琪](https://www.bilibili.com/video/BV1X7411F744)
    - [课程主页](https://sites.cs.ucsb.edu/~lingqi/teaching/games101.html)
    - 算是计算机图形学理论入门教程 讲的是数学和算法
- [Bilibili | GAMES104-现代游戏引擎：从入门到实践](https://www.bilibili.com/video/BV1oU4y1R7Km/)
    - [课程主页 - games](http://games-cn.org/games104/)
    - [课程主页 - boomingtech](https://games104.boomingtech.com/sc/course-list/)
    - [GitHub | Pilot](https://github.com/BoomingTech/Pilot)
    - 主要讲授游戏系统的各个方面 较基础

### 其他

- Completed [Bilibili | BIM应用开发科普04计算机图形学](https://www.bilibili.com/video/BV17f4y1G7AE)
    - 如果注重软件开发和相关背景可以通过这个视频了解
- Completed [Bilibili | GPU是如何工作的？Shader图形编程入门 - 奇乐编程学院](https://www.bilibili.com/video/BV1eE411E7Jf)
- 【看到 shader vs material】[YouTube | Shader Basics, Blending & Textures Shaders for Game Devs - Freya Holmér](https://youtu.be/kfM-yu0iQBk)
- Completed [常用三维文件解析](https://all3dp.com/2/most-common-3d-file-formats-model/)
    - 非常详细的说了三维文件里面都存了什么东西
    - Blender Export
        - .dae default ISO standard
        - .stl 只有模型的网格信息（三角形）
        - .obj 模型的Mesh、Material、Texture(单独存储在.mtl文件中) 不能存储动画
        - .fbx 模型的全部信息 包括动画

## 学习笔记

- Shader输入：Mesh Matrix4x4 Colors Values Textures
- VertexShader：只有两种作用：改变Vertex的位置 传数据给FragmentShader
- VertexShader对Mesh中的每一个顶点并行作用 在最终三角形Rasterizing之后 FragmentShader为每个像素上色
- FragmentShader：为什么叫Fragment而不是Pixel，这是因为Pixel往往是与你的屏幕上的像素一一对应的，比如我现在的电脑屏幕是2560×1600。但如果我看一个1080x1920的视频全屏，这时，1080p的视频的一个小色块对应一个Fragment，这些所有的Fragment可能还要经过一些变化才能成为真正屏幕上显示的Pixel（不一定对但大概是这个意思）
