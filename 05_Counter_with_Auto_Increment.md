# Counter with Auto Increment

## `main.dart`

```dart
import 'dart:async';
import 'package:flutter/material.dart';

void main() {
  runApp(MyMainApp());
}

class MyMainApp extends StatefulWidget {
  const MyMainApp({super.key});
  @override
  State<MyMainApp> createState() => MyMainAppState();
}

class MyMainAppState extends State<MyMainApp> {
  int count = 0;
  Timer? timer;

  void start() {
    pause();
    timer = Timer.periodic(const Duration(seconds: 1), (timer) {
      setState(() {
        count += 1;
      });
    });
  }

  void pause() {
    timer?.cancel();
  }

  void stop() {
    timer?.cancel();
    setState(() {
      count = 0;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        body: Center(
          child: Column(
            mainAxisAlignment: .center,
            children: [
              Text(count.toString(), style: TextStyle(fontSize: 40)),
              SizedBox(height: 30),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  ElevatedButton(onPressed: start, child: Text("Start")),
                  SizedBox(width: 20),
                  ElevatedButton(onPressed: pause, child: Text("Pause")),
                  SizedBox(width: 20),
                  ElevatedButton(onPressed: stop, child: Text("Stop")),
                ],
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/5.png" alt="Email Validation" style="width:50%;">
