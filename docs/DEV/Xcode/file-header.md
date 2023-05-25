# Xcode 自定义新建文件注释

打开`Finder`，⇧⌘G 前往 `~/Library/Developer/Xcode/UserData`

创建或修改`IDETemplateMacros.plist`的内容为：

```plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>FILEHEADER</key>
<string> ___FILENAME___</string>
</dict>
</plist>
```

保存后在Xcode中创建新文件，即可得到最简单的只有文件名而没有其他信息的注释

若要自定义内容，修改`<string> </string>`字段即可
