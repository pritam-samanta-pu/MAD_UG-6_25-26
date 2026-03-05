# Dynamic Cards Generator

## `main.dart`

```dart
import 'package:flutter/material.dart';
void main(){
  runApp(MaterialApp(
    debugShowCheckedModeBanner: false,
    home:InputPage(),
  ));
}
class InputPage extends StatefulWidget{
  const InputPage({super.key});
  @override
  State<InputPage> createState() {
    return InputPageState();
  }
}
class InputPageState extends State<InputPage>{
  final myController=TextEditingController();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Padding(
            padding: EdgeInsets.all(30),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                TextField(
                  controller: myController,
                  keyboardType: TextInputType.number,
                  decoration: InputDecoration(
                    labelText: "Enter a number",
                    border: OutlineInputBorder()
                  ),
                ),
                SizedBox(height: 20),
                ElevatedButton(
                    onPressed: (){
                      int n=int.parse(myController.text);
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (_) => SecondPage(count:n),
                        ),
                      );
                    },
                    child: Text("Generate Card")
                )
              ],
            ),
        ),
      ),
    );
  }
}
class SecondPage extends StatelessWidget{
  final int count;
  SecondPage({super.key,required this.count});
  final colors=[
    Colors.red,
    Colors.orange,
    Colors.yellow,
    Colors.green,
    Colors.blue,
    Colors.indigo
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("$count Card"),
      ),
      body: ListView.builder(
          itemCount: count,
          padding: EdgeInsets.all(23),
          itemBuilder: (_,ind){
            return Card(
              color: colors[ind%colors.length],
              margin: EdgeInsets.only(bottom: 15),
              child: ListTile(
                leading: CircleAvatar(
                  child: Text("${ind+1}"),
                ),
                title: Text("Card ${ind+1}"),
                subtitle: Text("This is card ${ind+1}."),
              ),
            );
          }),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/10.png" alt="Dynamic Cards Generator" style="width:50%;">
<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/10b.png" alt="Dynamic Cards Generator" style="width:50%;">
