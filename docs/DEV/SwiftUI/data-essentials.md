# Apple Developer Notes | Data Essentials in SwiftUI

## Instantiate a Model Object in a View

Connect `data to show in views` with `data defined in Model`.

**Model class:**

```swift
class Book: ObservableObject {
	/// @Published: Once title changed, Views related with Book refreshed.
	/// @Published works when this class is an ObservableObject
    @Published var title = "Great Expectations" 
}
```

**SwiftUI codes:**

```swift
struct LibraryView: View {
    @StateObject var book = Book() // Book is a class conforming to ObservableObject. Only instantiating uses `@StateObject`
    
    var body: some View {
        BookView(book: book)
    }
}

struct BookView: View {
    @ObservedObject var book: Book // Here book is not an instance of Model. So yse @ObservedObject

    // ...
}
```

## Share an Object Throughout the App

Save your time to pass arguments again and again if there are plenty of layers.

```swift
@main
struct BookReader: App {
    @StateObject var library = Library() // initiate ObservableObject with `@StateObject`
    
    var body: some Scene {
        WindowGroup {
            LibraryView()
                .environmentObject(library) // Here pass `library` to all sub-views of LibraryView().
        }
    }
}
```

```swift
struct LibraryView: View {
    @EnvironmentObject var library: Library // Get that EnvironmentObject
    
    // ...
}
```

## Manage Mutable Values

〇 当层View中需要更改的值定义为`@State var`(因为要保存这个值，而不是每次refresh UI的时候值都回到初始值)

〇 当层View使用的不可更改的值，定义该值为`let`


〇 当层View需要给下层View传值、且下层View只是使用而不改变该值，下层View中定义该值为`var`

〇 当层View需要给下层View传值、且下层View会改变该值，下层View中定义该值为`@Binding var`，确保下层View改的是当层View值的引用（改的是同一个）；当层View传递时写`$foo`

〇 某值只有当层和subView用，加`private`，上层View无法访问到该量
    
```swift
struct PlayerView: View {
    let episode: Episode
    @State private var isPlaying: Bool = false
    
    var body: some View {
        VStack {
            Text(episode.title)
            Text(episode.showTitle)
            PlayButton(isPlaying: $isPlaying) // Pass a binding.
        }
    }
}
```

```swift
struct PlayButton: View {
    @Binding var isPlaying: Bool
    
    var body: some View {
        Button(action: {
            self.isPlaying.toggle() // change isPlaying in sub-view. So use @Binding
        }) {
            Image(systemName: isPlaying ? "pause.circle" : "play.circle")
        }
    }
}
```

## References

〇 Main

[Apple Developer Documentation | Managing Model Data in Your App](https://developer.apple.com/documentation/swiftui/managing-model-data-in-your-app)

[Apple Developer Documentation | Managing User Interface State](https://developer.apple.com/documentation/swiftui/managing-user-interface-state)

[WWDC20 | Data Essentials in SwiftUI](https://developer.apple.com/wwdc20/10040)

〇 Secondary

[Apple Developer Documentation | State and Data Flow](https://developer.apple.com/documentation/swiftui/state-and-data-flow)