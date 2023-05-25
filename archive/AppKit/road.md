# 我的 Apple app 开发之路

210708

其实呢，我最初想学软件开发，是为了能够给macOS开发APP，因为我热爱着这个平台，想在上面创造一些能被全世界使用的APP。

然而YouTube上根本没有太多的macOS APP开发教程，因为苹果平台的主要开发还是iOS APP。但我想着这两个平台的APP构建应该差不多吧，先学iOS开发，之后应该很快就能上手macOS开发。

我开始学习iOS开发是2021年2月，选择的课程是Stanford cs193p，虽然当时已经有SwiftUI 2，但由于课程课程安排，使用的是SwiftUI 1，但这并不本质，思想是差不多的。SwiftUI真的很快可以上手，声明式UI，代码敲起来，模块化，再加上Apple加的例如动画的buff，写起来超级方便，表现也非常好。

事实上，SwiftUI 2是SwiftUI的一个很重大的里程碑，实现了SwiftUI管理APP的全部生命周期，这意味着你可以只用SwiftUI建立完整的APP。而且SwiftUI是全平台的，虽说是跨平台，它也根据不同的平台做了优化，反正都是苹果自己的系统。

如果你用SwiftUI构建一般的应用界面，是非常爽的一件事情。但真正用过SwiftUI开发的人肯定都知道，做iOS APP还得融合UIKit。但事实上，在目前看来，我接触的iOS端开发，一个工程的大部分使用SwiftUI，小部分加入UIKit，这是完全可以接受的；这也是目前来讲小团队开发iOS APP最便捷的方式。

但是如果平台更换到macOS，就有很大的不同。macOS上的操作和iOS、iPadOS操作的差异是非常大的，如果想要在macOS上开发应用，我觉得了解系统底层、对应用作优化是非常有必要的；而且macOS上有很多很多的扩展，一般支持更多的自定义操作，所有的这些，都很难用SwiftUI来完成。在这方面SwiftUI也有一个自己的问题，就是虽然文档写的很好，但是概念文档却没有官方的。

我也很想用SwiftUI，我也一直在鼓励大家使用SwiftUI，然而今年的WWDC21挺让我心凉的，感觉SwiftUI 3并没更新太多东西。这也是很大的问题，一年一次的更新让SwiftUI的发展很缓慢，这一点让人捉急。就算现在可以说，SwiftUI就是未来苹果平台UI构建的趋势，但谁也没法说这个未来什么时候、几年后才能到来，总不能一直让人等吧？

那么开发macOS APP用什么，用AppKit，或者说Cocoa（Apple不可能将AppKit和UIKit抛弃，事实上现在也在不断推出新的功能）。当然你可以将SwiftUI和AppKit融合起来，但这个……没什么人做，没什么教程，也没有什么官方的参考，你能做的就只是猜测把两个东西融合起来会发生什么…你也不知道里面的东西如何运作，除非你很的特别强，能够完全理解两套框架的生命周期和与系统的交互方式。（在我之前开发Menu Bar APP的时候就感觉融合很不适应）

回到最初的想法——我要开发macOS APP。那么，用AppKit是肯定的了。语言有两种选择，Swift和OC；肯定选Swift，现代的语言，API都支持，这两点就够了。UI如何构建呢？Storyboard看起来是14年推出的，很方便，但问题太多了：版本控制查看diff和解决conflict看XML肯定不行吧，追求快速构建还用鼠标拖来拖去肯定也不行吧；纯UI构建对于我来说，应该是很适合的，决定选择这方面，我也熟悉用代码构建UI的这一套流程。最好的希望是，能够在AppKit中融合SwiftUI，这样可能才是最好的开发方式吧。

总结一下，对于我来说——
开发iOS APP，以小团队的角度来看，使用SwiftUI，只支持最新的iOS系统。做不到的功能找教程融合UIKit；如果UIKit都做不到，那说明这个APP也许不适合做成iOS平台的APP。
开发macOS APP，先考虑功能：如果只是点击，和数据进行交互，SwiftUI完全可以胜任；但是一旦要考虑定制化，SwiftUI直接吃瘪，纯AppKit构建一定能省去很多莫名其妙的问题。如果遇到AppKit还做不出来的东西，那肯定是开发者学的东西不够多吧；不然就Apple背锅喽。

所以，虽然YouTube macOS纯代码UI开发的教程开发少之又少，还是打算尽可能去学。Waiting for my creative apps.

PS. 对于初学者来说，学个Swift和SwiftUI，够了。别想着做这以外更多的事情，如果想做更多的事情，和我一样，写这样的分析，考虑自己的需求，选取合适的学习路径，再开始自己的开发之路吧。

## References

- Storyboard vs Code - Why I use Storyboards
    - https://youtu.be/MruN43jw8GU
    - 重要观点：
        - 适合纯代码那就纯代码UI
        - 初学者选择 StoryBoard / SwiftUI 更直观
- Storyboards vs. Coded UI vs. SwiftUI - Which is the best way to build the UI for iOS apps? (2020)
    - https://youtu.be/17cyRUi8iu8
    - 重要观点：
        - SwiftUI做工程APP只能等
