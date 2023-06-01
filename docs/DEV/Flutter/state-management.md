# App State Management

## Provider 黑夜模式案例

`lib/main.dart`

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        body: ChangeNotifierProvider(
          create: (context) => ThemeModel(),
          child: MyPage(),
        ),
      ),
    ),
  );
}

class ThemeModel extends ChangeNotifier {
  bool isDarkModeOn = false;

  void toggleDarkMode() {
    isDarkModeOn = !isDarkModeOn;
    notifyListeners();
  }
}

class MyPage extends StatelessWidget {
  MyPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Consumer<ThemeModel>(
      builder: (context, model, child) {
        return GestureDetector(
          onTap: () {
            model.toggleDarkMode();
          },
          child: Container(
            color: model.isDarkModeOn ? Colors.black : Colors.white,
            child: Center(
              child: Text(
                "Hello, world!",
                style: TextStyle(
                  color: model.isDarkModeOn ? Colors.white : Colors.black,
                  fontSize: 36,
                ),
              ),
            ),
          ),
        );
      },
    );
  }
}
```

## References

- https://docs.flutter.dev/development/data-and-backend/state-mgmt/simple
