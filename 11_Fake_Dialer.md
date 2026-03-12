# Fake Dialer

## `main.dart`

```dart
import 'package:flutter/material.dart';

void main() =>
    runApp(MaterialApp(home: Dialer(), debugShowCheckedModeBanner: false));

class Dialer extends StatelessWidget {
  final controller = TextEditingController();

  Dialer({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Dialer')),
      body: Padding(
        padding: EdgeInsets.all(20),
        child: Column(
          children: [
            TextField(
              controller: controller,
              keyboardType: TextInputType.phone,
              decoration: InputDecoration(labelText: 'Enter phone number'),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              child: Text('Call'),
              onPressed: () {
                showDialog(
                  context: context,
                  builder: (_) => AlertDialog(
                    title: Text('Calling...'),
                    content: Text(controller.text),
                    actions: [
                      TextButton(
                        child: Text('End Call'),
                        onPressed: () => Navigator.pop(context),
                      ),
                    ],
                  ),
                );
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/11.png" alt="Fake Dialer" style="width:50%;">
