# Unity Notes

## 学习资料

- [Unity | Documentation](https://docs.unity3d.com/Manual/index.html)
- Completed [Bilibili | 10分钟了解游戏制作的全过程 游戏是如何开发出来的 - 奇乐编程学院](https://www.bilibili.com/video/BV1xJ41197e9)
- Completed [YouTube | Everything to know about the PARTICLE SYSTEM](https://www.youtube.com/watch?v=FEA1wTMJAR0)
    - 粒子效果介绍 就是一堆例子呈现在三维空间中的效果 想要很酷炫的话 你可以给粒子加上颜色、模型、物理、发光、时变等多种效果

### 其他

- Completed [Bilibili | Unity 10分钟快速入门 - 奇乐编程学院](https://www.bilibili.com/video/BV1PL4y1e7hy)
    - 讲的清楚但完全不够用 只是个简介

## 学习笔记

### Mesh Material Shader Texture 辨析

- Mesh 三维物体的轮廓（网格）
    - 我的理解就是物体的位置 Mesh由多个三角形构成 一个三角形在空间中就表示一个位置上的小面 然后你要往这个面上面放什么颜色 放什么图片 确定这个三角形与背景的作用、最终到屏幕上加的后处理。总之这个小的三角形就是第一步 确定位置
- Material 渲染方式和参数（材质球）
- Shader 渲染的算法（着色器）
- Texture 图片 增加颜色细节（贴图）
    - 把Texture按照Mesh切分成多个三角形 然后一个一个放到Mesh的位置上 然后玩家看到的实际东西是一个三角形里面的Texture的图 而不是很多个三角形分别做的渲染
    - 举个例子：我的世界 一个方块的一个正方形面 就是两个三角形 你通过更换Texture来更换这个正方形面上的东西 而不是将这个正方形面切成很多个三角形 然后一个三角形一个三角形去渲染
- Normal 增加物体的凹凸细节等（法线等其他贴图）
- AnimationClip 让物体动起来（动画）

### 鼠标拖拽物体在平面上移动

- 新建一个项目
- 在场景中添加一个平面（地面） 添加一个物体
- 新建下面的脚本 将脚本拖放到物体上

```cs
// 鼠标拖拽物体在平面上移动（不超过边界）
// References: https://jingyan.baidu.com/article/fa4125ac076ed628ac7092d2.html

using UnityEngine;

public class DragByMouse : MonoBehaviour
{
    // 鼠标一动就调用这个函数
    void OnMouseDrag()
    {
        // 获得从Camera开始到屏幕上的点的光线
        Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
        // 让这条光线射出去 得到所有的碰撞信息
        RaycastHit[] hits;
        hits = Physics.RaycastAll(ray); // 返回的hits是乱序的
        for (int i = 0; i < hits.Length; i++)
        {
            // 找到与Plane的碰撞信息
            if (hits[i].collider.name == "Plane")
            {
                Debug.Log($"鼠标点击的位置 {Input.mousePosition}"); // 只能精确到一个像素点
                Debug.Log($"光线与平面碰撞的位置 {hits[i].point}"); // 注意坐标系 相当于二维坐标xy再加一个深度z
                Debug.Log($"物体移动前的位置 {transform.position}");

                // 使用该碰撞信息重新设置物体的位置 这里只是在物体所在的平面xz上移动
                transform.position = new Vector3(hits[i].point.x, transform.position.y, hits[i].point.z);

                Debug.Log($"物体移动后的位置 {transform.position}");
                break;
            }
        }
    }
}
```
