# Cocoa 新建项目的方式

> macOS 12.0.1 Xcode 13.1 Swift 5.5.1

不考虑使用StoryBoard。保留MainMenu。

新建项目：Xcode -> New -> Project... -> macOS.Application.App -> Interface: XIB & Language: Swift
删除自带的Window：MainMenu.xib -> ProjectName(Window) selected and hit delete -> delete the code `@IBOutlet var window: NSWindow!` in AppDelegate.swift

接下来有两种方式，使用NIB相当于自己可视化的建立了一个新的Window，用继承NSWindowController的控制器来控制NIB中不能/难以/可以调整的属性。在纯代码的实现方式中，WindowController有点多余，因为一般NSWindowController是用来控制NIB file的；可以只继承Window然后在入口中显示这个Window。

## 新建NIB再使用WindowController进行控制

https://www.youtube.com/watch?v=Xy0-x-Zf1YE

新建ViewController

* cmd N -> macOS.Source.Cocoa Class
* Class: MainWindowController & Subclass of: NSWindowController & Also create XIB file for user interface & language: Swift

```swift
// AppDelegate.swift

import Cocoa

@main
class AppDelegate: NSObject, NSApplicationDelegate {
    let mainWindowController = MainWindowController()

    func applicationDidFinishLaunching(_: Notification) {
        mainWindowController.showWindow(nil)
    }

    func applicationWillTerminate(_: Notification) {}

    func applicationSupportsSecureRestorableState(_: NSApplication) -> Bool {
        return true
    }
}
```

```swift
// MainWindowController.swift

import Cocoa

class MainWindowController: NSWindowController {
    convenience init() {
        self.init(windowNibName: "MainWindowController")
    }

    override func windowDidLoad() {
        super.windowDidLoad()

        window?.titlebarAppearsTransparent = true
        window?.titleVisibility = .hidden
    }
}
```

## 不使用NIB代码添加Window

```swift
// AppDelegate.swift

import Cocoa

@main
class AppDelegate: NSObject, NSApplicationDelegate {
    let mainWindowController = MainWindowController()

    func applicationDidFinishLaunching(_: Notification) {
        mainWindowController.showWindow(nil)
    }

    func applicationWillTerminate(_: Notification) {}

    func applicationSupportsSecureRestorableState(_: NSApplication) -> Bool {
        return true
    }
}
```

```swift
// MainWindowController.swift

import Cocoa

class MainWindowController: NSWindowController {
    convenience init() {
        self.init(window: MainWindow())
        // use MainWindowController to control a MainWindow()
        // MainWindow is like a NIB file that construct a window
    }

    override func windowDidLoad() {
        super.windowDidLoad()
    }
}
```

```swift
// MainWindow.swift

import Cocoa

class MainWindow: NSWindow {
    convenience init() {
        let styleMask: NSWindow.StyleMask = [.titled, .closable, .miniaturizable, .resizable]
        self.init(
            /// set it after initializing
            contentRect: .zero,
            /// You cannot use `[]` here and use `self.styleMask = [.titled, ...]` after it, which may cause effect losing, though in documentation `NSWindow.styleMask`, Apple says that "setting this property has the same restrictions as the styleMask parameter of `init(contentRect:styleMask:backing:defer:)`".
            styleMask: styleMask,
            /// only `.buffered` is supported
            backing: .buffered,
            /// "Deferring the creation of the window improves launch time and minimizes the virtual memory load on the window server."
            defer: true
        )

        self.title = "Main Window"
        self.setFrameOrigin(.init(x: 100, y: 100))
        self.setContentSize(.init(width: 300, height: 400))
    }
}
```

## 只使用Window并在mian入口中显示

工程较大时不推荐。修改`AppDelegate.swift`：

```swift
// AppDelegate.swift

import Cocoa

@main
class AppDelegate: NSObject, NSApplicationDelegate {
//    let mainWindowController = MainWindowController()
    let mainWindow = MainWindow()

    func applicationDidFinishLaunching(_: Notification) {
//        mainWindowController.showWindow(nil)
        mainWindow.setIsVisible(true)
    }

    func applicationWillTerminate(_: Notification) {}

    func applicationSupportsSecureRestorableState(_: NSApplication) -> Bool {
        return true
    }
}
```

## 不使用Controller

事实上，Controller都是View Management中的东西：Manage your user interface, including the size and position of views in a window. 我们只需要添加window和view就好了

```swift
// AppDelegate.swift

import Cocoa

@main
class AppDelegate: NSObject, NSApplicationDelegate {
    // MARK: - Application

    func applicationDidFinishLaunching(_: Notification) {
        CreateAndShowMainWindow()
    }

    func applicationShouldTerminateAfterLastWindowClosed(_: NSApplication) -> Bool {
        true
    }

    // MARK: - Windows

    /// main window
    let mainWindow = MainWindow()
    func CreateAndShowMainWindow() {
        mainWindow.makeKeyAndOrderFront(nil) // shows the window
    }
}
```

```swift
// MainWindow.swift

import Cocoa

class MainWindow: NSWindow {
    // MARK: - Window

    convenience init() {
        let styleMask: NSWindow.StyleMask = [.titled, .closable, .miniaturizable, .resizable]
        self.init(
            /// set it after initializing
            contentRect: .zero,
            /// You cannot use `[]` here and use `self.styleMask = [.titled, ...]` after it, which may cause effects losing, though in documentation `NSWindow.styleMask`, Apple says that "setting this property has the same restrictions as the styleMask parameter of `init(contentRect:styleMask:backing:defer:)`".
            styleMask: styleMask,
            /// only `.buffered` is supported
            backing: .buffered,
            /// "Deferring the creation of the window improves launch time and minimizes the virtual memory load on the window server."
            defer: true
        )

        ConfigureWindow()

        AddMainView()
    }

    func ConfigureWindow() {
        self.title = "Main Window"
        self.setFrameOrigin(.init(x: 100, y: 100))
        self.setContentSize(.init(width: 300, height: 400))
    }

    // MARK: - Views

    /// main view
    let mainView = MainView()
    func AddMainView() {
        self.contentView = mainView
    }
}
```

```swift
// MainView.swift

import Cocoa

class MainView: NSView {
    // MARK: - View

    override func draw(_ dirtyRect: NSRect) {
        super.draw(dirtyRect)
        AddLabel()
    }

    // MARK: - Subviews

    /// label
    let myLabel: NSView = NSTextField(labelWithString: "my label")
    func AddLabel() {
        self.addSubview(myLabel)
    }
}
```

### 进一步优化

```swift
// AppDelegate.swift

import Cocoa

@main
class AppDelegate: NSObject, NSApplicationDelegate {
    // MARK: - Application

    func applicationDidFinishLaunching(_: Notification) {
        CreateAndShowMainWindow()
    }

    func applicationShouldTerminateAfterLastWindowClosed(_: NSApplication) -> Bool {
        true
    }

    // MARK: - Windows

    /// main window
    let mainWindow = MainWindow()
    func CreateAndShowMainWindow() {
        mainWindow.makeKeyAndOrderFront(self) // shows the window
        mainWindow.center()
    }
}
```

```swift
// MainWindow.swift

import Cocoa

class MainWindow: NSWindow {
    // MARK: - Window

    convenience init() {
        let styleMask: NSWindow.StyleMask = [.titled, .closable, .miniaturizable, .resizable]
        self.init(
            /// set it after initializing
            contentRect: .zero,
            /// You cannot use `[]` here and use `self.styleMask = [.titled, ...]` after it, which may cause effects losing, though in documentation `NSWindow.styleMask`, Apple says that "setting this property has the same restrictions as the styleMask parameter of `init(contentRect:styleMask:backing:defer:)`".
            styleMask: styleMask,
            /// only `.buffered` is supported
            backing: .buffered,
            /// "Deferring the creation of the window improves launch time and minimizes the virtual memory load on the window server."
            defer: true
        )

        ConfigureWindow()

        AddMainView()
    }

    func ConfigureWindow() {
        self.title = "Main Window"
        self.setContentSize(.init(width: 300, height: 400))
    }

    // MARK: - Views

    /// main view
    let mainView = MainView()
    func AddMainView() {
        self.contentView = mainView // 这里设置contentView应该会改变mainView的属性，比如mainView的frame变成了窗口的contentSize
    }
}
```

```swift
// MainView.swift

import Cocoa

class MainView: NSView {
    // MARK: - View

    convenience init() {
        self.init(frame: .zero)

        ConfigureView()

        AddLabel()
    }

    func ConfigureView() {
        self.wantsLayer = true
        self.layer?.backgroundColor = NSColor.orange.cgColor
    }

    // MARK: - Subviews

    /// label
    let myLabel: NSView = NSTextField(labelWithString: "my label")
    func AddLabel() {
        myLabel.frame = .init(x: 30, y: 0, width: 100, height: 20)
        myLabel.wantsLayer = true
        myLabel.layer?.backgroundColor = NSColor.green.cgColor
        self.addSubview(myLabel)
    }
}
```
