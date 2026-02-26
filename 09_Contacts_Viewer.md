# Contacts Viewer

## `main.dart`

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(colorSchemeSeed: Colors.teal),
      home: ContactApp(),
    );
  }
}

class ContactApp extends StatelessWidget {
  ContactApp({super.key});

  final List<Map<String, String>> contacts = [
    {'name': 'John Doe', 'phone': '555-0101'},
    {'name': 'Jane Smith', 'phone': '555-0102'},
    {'name': 'Bob Johnson', 'phone': '555-0103'},
    {'name': 'Alice Williams', 'phone': '555-0104'},
    {'name': 'John Doe', 'phone': '555-0101'},
    {'name': 'Jane Smith', 'phone': '555-0102'},
    {'name': 'Bob Johnson', 'phone': '555-0103'},
    {'name': 'Alice Williams', 'phone': '555-0104'},
    {'name': 'John Doe', 'phone': '555-0101'},
    {'name': 'Jane Smith', 'phone': '555-0102'},
    {'name': 'Bob Johnson', 'phone': '555-0103'},
    {'name': 'Alice Williams', 'phone': '555-0104'},
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Contact App"),
        backgroundColor: Colors.teal,
        foregroundColor: Colors.white,
      ),
      body: ListView.builder(
        itemCount: contacts.length,
        itemBuilder: (context, ind) {
          final contact = contacts[ind];
          return ListTile(
            leading: CircleAvatar(
              backgroundColor: Colors.teal,
              foregroundColor: Colors.white,
              child: Text(contact["name"]![0]),
            ),
            title: Text(contact["name"]!),
            subtitle: Text(contact["phone"]!),
            trailing: Icon(Icons.phone, color: Colors.teal),
          );
        },
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/9.png" alt="Contacts Viewer" style="width:50%;">
