# App State Management

> Reference to <https://docs.flutter.dev/development/data-and-backend/state-mgmt/simple>.

`main.dart`

```dart
import 'package:provider/provider.dart';

import 'package:flutter/material.dart';

class MyModel extends ChangeNotifier {
  bool isOperating = false; // source of states

  void startOperating() {
    isOperating = true;
    notifyListeners(); // re-build widgets
  }

  void endOperating() {
    isOperating = false;
    notifyListeners(); // re-build widgets
  }
}

void main() {
  runApp(
    MaterialApp(
      home: Scaffold(
        body: ChangeNotifierProvider( // put `ChangeNotifierProvider` above the widgets that need to access it
          create: (context) => MyModel(),
          child: ContextView(),
        ),
      ),
      debugShowCheckedModeBanner: false,
    ),
  );
}

class ContextView extends StatelessWidget {
  ContextView({super.key});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Consumer<MyModel>( // use `Consumer` to get the model in `builder`
        builder: (context, model, child) {
          if (model.isOperating) {
            return ElevatedButton(
                onPressed: () {
                  model.endOperating(); // call function from the model (to update widgets)
                },
                child: Text("End Operating"));
          } else {
            return ElevatedButton(
                onPressed: () {
                  model.startOperating(); // call function from the model (to update widgets)
                },
                child: Text("Start Operating"));
          }
        },
      ),
    );
  }
}
```
