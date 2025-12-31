# Simple Login UI

## `main.dart`

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MainApp());
}

class MainApp extends StatelessWidget {
  const MainApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(debugShowCheckedModeBanner: false, home: LoginPage());
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});

  @override
  State<LoginPage> createState() => LoginPageState();
}

class LoginPageState extends State<LoginPage> {
  final TextEditingController userCtr = TextEditingController();
  final TextEditingController passCtr = TextEditingController();
  void loginFn() {
    if (userCtr.text.isNotEmpty && passCtr.text.isNotEmpty) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text("Welcome!"), backgroundColor: Colors.green),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("MyApp")),
      body: Padding(
        padding: EdgeInsets.all(30),
        child: Column(
          mainAxisAlignment: .center,
          children: [
            TextField(
              controller: userCtr,
              decoration: InputDecoration(labelText: "UserName"),
            ),
            SizedBox(height: 30),
            TextField(
              controller: passCtr,
              obscureText: true,
              decoration: InputDecoration(labelText: "Password"),
            ),
            SizedBox(height: 30),
            ElevatedButton(onPressed: loginFn, child: Text("Login")),
          ],
        ),
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/2.png" alt="Simple Login UI" style="width:50%;">
