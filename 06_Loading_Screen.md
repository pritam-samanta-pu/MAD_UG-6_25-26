# Loading Screen (Progress Bar)

## `main.dart`

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  const MyApp({super.key});
  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  double process = 0;
  String msg = "Click on Start";
  void handleLoading() async {
    setState(() {
      process = 0;
      msg = "Content is loading...";
    });
    for (int i = 0; i <= 100; i++) {
      await Future.delayed(const Duration(milliseconds: 75));
      setState(() {
        process = i / 100;
      });
    }
    setState(() {
      msg = "Finished🎉";
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              LinearProgressIndicator(value: process),
              SizedBox(height: 25),
              Text("${(process * 100).toInt()}%"),
              SizedBox(height: 25),
              Text(msg),
              SizedBox(height: 25),
              ElevatedButton(onPressed: handleLoading, child: Text("Start")),
            ],
          ),
        ),
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/6.jpg" alt="Loading Screen (Progress Bar) " style="width:50%;">
