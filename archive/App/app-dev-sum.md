# Summary of App Dev Framework

From an indie's perspective:

## Choices

Mobile

- iOS / Android
    - Browser
        - 显示内容 简单交互
    - Flutter (offline)
        - 简单应用
- iOS
    - SwiftUI
        - 需要用到 iOS SDK 如无线传输 / Apple Pencil 等功能
        - 从开发的角度 SwiftUI相比UIkit好写太多

Desktop

- Windows / Linux / macOS
    - 我感觉在中国Linux发行版接下来二十年是有比较大的潜力的 有比较大的市场
    - Browser
        - 显示内容 简单交互
        - 在线编辑器
            - 各种设计类的工具软件都可以搬到浏览器里面
    - Qt + C++
        - 工业级应用
    - Flutter
        - 简单应用
- macOS
    - SwiftUI
        - 简单应用
    - AppKit
        - 专业的效率应用

Game

- Unity
- Unreal Engine
- Cocos

## TOTRY

- Cloud Functions (serverless)
- HTML5/CSS3/JS

## Web

- Frontend
    - HTML&CSS&JS （传统解决方案）
    - React / Vue （现代框架）
- Backend
    - Serverless Cloud Functions （在云厂商对的平台写后端 不需要Linux服务器操作）
    - Hasura （点几下GUI建表 不需要Linux服务器操作）
    - Django （现代框架 需要在Linux服务器部署）

## Native - Mobile

- iOS
    - Xcode + UIKit + Swift （Imperative UI）
    - Xcode + SwiftUI + Swift （Declarative UI）
- Android
    - Android Studio + Java
    - Android Studio + Kotlin
- React Native + JS / Flutter + Dart

## Native - Desktop

- macOS
    - Xcode + AppKit + Swift （Imperative UI）
    - Xcode + SwiftUI + Swift （Declarative UI）
- Windows
    - Visual Studio
- Linux
    - Qt + C++
    - PyQt + Python
- Electron + JS / Flutter + Dart
