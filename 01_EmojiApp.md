# Hello Flutter Emoji App

## `main.dart`

```dart
import 'package:flutter/material.dart';
import 'dart:math';

void main(){
  runApp(const MainApp());
}
class MainApp extends StatelessWidget{
  const MainApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: EmojiApp(),
    );
  }
}

class EmojiApp extends StatefulWidget{
  const EmojiApp({super.key});
  @override
  State<EmojiApp> createState() => EmojiBody();
}
class EmojiBody extends State<EmojiApp>{
  List<String> emjArray=['😑','🫤','🥹','🧐','👾','🙈','🐻‍❄️','🧟','🕷️','🐦‍🔥','🐍','🦙','🐈‍⬛','🐾','🤒','🤑','🎉'];
  var random=Random();
  String currEmj='✨';
  void changeEmj(){
    setState(() {
      currEmj=emjArray[random.nextInt(emjArray.length)];
    });
  }
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("EmojiApp"),),
      body: Center(
        child: Column(
          mainAxisAlignment: .center,
          children: [
          Text(currEmj,style: TextStyle(fontSize: 150),),
          SizedBox(height: 150,),
          ElevatedButton(onPressed: changeEmj, child: Text("Change Emoji"))
        ],),
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/1.png" alt="Hello Flutter Emoji App" style="width:50%;">
