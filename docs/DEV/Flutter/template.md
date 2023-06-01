# Flutter Project Template

`lib/main.dart`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        body: ContentWidget(),
      ),
    ),
  );
}

class ContentWidget extends StatelessWidget {
  ContentWidget({super.key});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text(
        "Hello, world!",
        style: TextStyle(fontSize: 36),
      ),
    );
  }
}
```
