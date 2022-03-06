# ExNotes Considerations and Learning

考虑：

- 不会使用PencilKit，因为定制化困难
- 不会使用Metal，因为代码写起来困难，资料少，很难debug
- 可以考虑PDFKit，也就是直接操作一个PDF
- 可以考虑Core Graphics，因为这就是Apple提供的矢量操作框架

## Metal

* <https://donaldpinckney.com/metal/2018/07/05/metal-intro-1.html#what-is-metal-and-why-use-it>
    * This blog clearly teach you to use Metal to draw a triangle on you screen step by step. really recommended
* <https://www.raywenderlich.com/7475-metal-tutorial-getting-started>
    * simple but enough

* WWDC
    * [WWDC14 | Working with Metal: Overview](https://developer.apple.com/wwdc14/603)
    * [WWDC14 | Working with Metal: Fundamentals](https://developer.apple.com/wwdc14/604)
    * [WWDC14 | Working with Metal: Advanced](https://developer.apple.com/wwdc14/605)

## Notability

Google搜索`apple pencil metal`，看到这个链接<https://apps.apple.com/us/story/id1586860080>，是关于NB的一个推荐。写道：

> Sketch, draw, and doodle with the app’s drawing features. Notability’s ink rendering engine has been freshly rewritten in Metal, which basically means everything is way faster now, including the app’s pencil, paint brushes, and texturing ink.

freshly rewritten in Metal，说明还是得使用底层的渲染框架来做到无延时。也就是WWDC19: Introducing to the PencilKit所说的步骤。

## Apple Pencil

* [WWDC19 | Introducing PencilKit](https://developer.apple.com/wwdc19/221)
    * The first xx minutes shows that you should using Metal and series of techs to lower the latency. It tells you how to exert full ability of Apple Pencil.
* <https://developer.apple.com/documentation/uikit/pencil_interactions>
    * Get data collected from sensors in Apple Pencil.

* [Sample Code | Leveraging Touch Input for Drawing Apps](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/leveraging_touch_input_for_drawing_apps)
* [Sample Code | Illustrating the Force, Altitude, and Azimuth Properties of Touch Input](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/illustrating_the_force_altitude_and_azimuth_properties_of_touch_input)
* [Article | Handling Input from Apple Pencil](https://developer.apple.com/documentation/uikit/pencil_interactions/handling_input_from_apple_pencil)

* [Core Graphics Tutorial: Getting Started](https://www.raywenderlich.com/8003281-core-graphics-tutorial-getting-started)
* [Apple Pencil Tutorial: Getting Started](https://www.raywenderlich.com/1407-apple-pencil-tutorial-getting-started)

## PencilKit

首先明确Apple推出的PencilKit：

* PencilKit 2019年推出，使用最简单的框架给开发者提供调用Apple Pencil绘图的方法
* 2020年升级，加入了可以自定义的Stroke。

只需要三行加入现有的view hierarchy。

```swift
let canvas = PKCanvasView(frame: .init(x: 0, y: 0, width: 600, height: 400))
view.addSubview(canvas)
canvas.tool = PKInkingTool(.pen, color: .black, width: 20)
```

但个人使用感觉很难用。默认的书写工具只提供`.pen`和`.pencil`，压感不强，书写形式较单一。而且由于使用了ML来预测笔画，书写提速时会发生画面抖动厉害的情况（不如不降低延迟）。即使是2020年引入了新的一些方法，我仍然不愿意使用PencilKit进行开发。

## Stroke

* https://stackoverflow.com/a/42891040/14298786
    * use vectors
    * [Wiki | Ramer–Douglas–Peucker algorithm](https://en.wikipedia.org/wiki/Ramer-Douglas-Peucker_algorithm)
    * <http://blog.ivank.net/interpolation-with-cubic-splines.html>
* [Adobe | What is vector art](https://www.adobe.com/creativecloud/illustration/discover/vector-art.html)
* https://developer.apple.com/documentation/uikit/uibezierpath
* https://en.wikipedia.org/wiki/Bézier_curve
* how computers draw cubic Bézier curves https://www.dev-metal.com/bezier-curves-hood-4min-video/
* GitHub <https://github.com/OwenCalvin/hand-drawing-swift-metal>
    * check <https://github.com/eldade/ios_metal_bezier_renderer>
* Rasterization in Metal https://www.reddit.com/r/GraphicsProgramming/comments/l412jf/rasterization_in_metal/ 
* UIBezierPath https://developer.apple.com/documentation/uikit/uibezierpath
* to render a model or make something smooth: https://www.reddit.com/r/GraphicsProgramming/comments/l412jf/rasterization_in_metal/
    * just split the shape into several triangles

**Raymarch**

Maybe you could raymarch a surface in a pixel shader. You could render a bounding geometry using triangles just to limit the number of pixels running the shader. That's done somewhat often for 2D curves, but I've not seen it done for 3D curved surfaces besides https://blog.demofox.org/2016/12/16/analyticsurfacesvolumesgpu/

SDF

* https://www.iquilezles.org/www/articles/distfunctions/distfunctions.htm
* https://www.labri.fr/perso/nrougier/python-opengl/#distance-based-anti-aliasing

* Nb上的一笔究竟是如何定义的？？是贝塞尔曲线直接围起来形成图形？还是把笔划的最中间的那条轨迹和每个轨迹点的粗度存起来？
    * 按照 https://stackoverflow.com/a/42891040/14298786 所说应该是中间点的轨迹
    * 如果是是贝塞尔曲线，那就Metal直接三角形绘制

## stroke

* 笔划的数据结构定义
* 笔划是怎么存储的
* 矢量是什么？字体如何渲染在屏幕上 How to show a vector on iOS screen
* 看一下PDF的标准，基本上和PDF一致吧

画一笔的过程：

* Pencil挨到屏幕，数据采集开始，收到第一个点，存储第一个点；
* Pencil开始滑动，收到第二个点；
* Pencil继续滑动，收到第三个点；
    * 如果第三个点离第二个点特别近，那么这个点不用记录
    * 如果第三个点与第二个点的连线 与 第一个点和第二点的连线的角度特别相似，那么这个点不用记录
    * 虽然说不用记录，但其实是不用存储第二个点，而是根据第二个点和第三个点的关系，存储第三个点附近的一个位置点。
    * 如果第三个点和前面的数据差的比较远，直接存储。
    * 注意这里说的都是位置，注意还要存储压力。
* Pencil继续滑动，收到第四个点；
    * 注意如果仍然按照上面的方法，第四个点是否存储取决于第四个点与 第二第三个点的关系。因此即使不存储第二第三个点，也应该在内存中留下
* Pencil离开屏幕，将存储的点真正进行存储
    * 注意之前步骤所说的存储是指，收集到的数据在一个数组，确定存储的数据在一个数组（小于收到的数据的数量）
    * 在Pencil完成一笔的时候，我们将确定存储的这些数据写入文件，完成一笔的绘制。

渲染过程：

* 差值为曲线即可
