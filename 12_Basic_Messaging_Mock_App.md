# Basic Messaging Mock App

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
      title: 'Messaging Mock App',
      home: ChatPage(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class ChatPage extends StatefulWidget {
  const ChatPage({super.key});

  @override
  State<ChatPage> createState() => ChatPageState();
}

class ChatPageState extends State<ChatPage> {
  TextEditingController messageController = TextEditingController();
  List<String> messages = [];

  void sendMessage() {
    if (messageController.text.isNotEmpty) {
      setState(() {
        messages.add(messageController.text);
        messageController.clear();
      });
    }
  }

  void clearMessages() {
    setState(() {
      messages.clear();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Basic Messaging App"),
        actions: [
          IconButton(icon: Icon(Icons.delete), onPressed: clearMessages),
        ],
      ),

      body: Column(
        children: [
          Expanded(
            child: ListView.builder(
              itemCount: messages.length,
              itemBuilder: (context, index) {
                return Container(
                  alignment: Alignment.centerRight,
                  padding: EdgeInsets.all(10),
                  child: Container(
                    padding: EdgeInsets.all(12),
                    decoration: BoxDecoration(
                      color: Colors.blue,
                      borderRadius: BorderRadius.circular(10),
                    ),
                    child: Text(
                      messages[index],
                      style: TextStyle(color: Colors.white),
                    ),
                  ),
                );
              },
            ),
          ),

          Row(
            children: [
              Expanded(
                child: Padding(
                  padding: EdgeInsets.all(8),
                  child: TextField(
                    controller: messageController,
                    decoration: InputDecoration(
                      hintText: "Type message",
                      border: OutlineInputBorder(),
                    ),
                  ),
                ),
              ),

              ElevatedButton(onPressed: sendMessage, child: Text("Send")),

              SizedBox(width: 5),

              ElevatedButton(
                onPressed: clearMessages,
                child: Text("Clear All"),
              ),
            ],
          ),
        ],
      ),
    );
  }
}

```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/12.png" alt="Basic Messaging Mock App" style="width:50%;">
