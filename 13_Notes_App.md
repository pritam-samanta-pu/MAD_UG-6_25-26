# Notes App

## Update `pubspec.yaml`

```dart
dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.2.2
```

## `main.dart`

```dart
import 'package:flutter/material.dart';
import 'dart:io';
import 'package:path_provider/path_provider.dart';

void main() =>  runApp(MaterialApp(home: NotesApp(), debugShowCheckedModeBanner: false));


class NotesApp extends StatefulWidget {
  const NotesApp({super.key});

  @override
  State<NotesApp> createState() => NotesAppState();
}

class NotesAppState extends State<NotesApp> {
  final _controller = TextEditingController();
  String _savedNote = '';

  Future<File> _getFile() async {
    final dir = await getApplicationDocumentsDirectory();
    return File('${dir.path}/note.txt');
  }

  Future<void> _saveNote() async {
    final file = await _getFile();
    await file.writeAsString(_controller.text);
    ScaffoldMessenger.of(
      // ignore: use_build_context_synchronously
      context,
    ).showSnackBar(SnackBar(content: Text('Note Saved!')));
  }

  Future<void> _readNote() async {
    final file = await _getFile();
    if (await file.exists()) {
      final content = await file.readAsString();
      setState(() => _savedNote = content);
    } else {
      setState(() => _savedNote = 'No note found!');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Notes App')),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              maxLines: 5,
              decoration: InputDecoration(
                labelText: 'Enter your note',
                border: OutlineInputBorder(),
              ),
            ),
            SizedBox(height: 10),
            Row(
              children: [
                Expanded(
                  child: ElevatedButton(
                    onPressed: _saveNote,
                    child: Text('Save Note'),
                  ),
                ),
                SizedBox(width: 10),
                Expanded(
                  child: ElevatedButton(
                    onPressed: _readNote,
                    child: Text('Read Note'),
                  ),
                ),
              ],
            ),
            SizedBox(height: 20),
            if (_savedNote.isNotEmpty)
              Container(
                width: double.infinity,
                padding: EdgeInsets.all(12),
                decoration: BoxDecoration(
                  color: Colors.yellow[100],
                  border: Border.all(color: Colors.amber),
                  borderRadius: BorderRadius.circular(8),
                ),
                child: Text(
                  'Saved Note:\n$_savedNote',
                  style: TextStyle(fontSize: 16),
                ),
              ),
          ],
        ),
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/13.png" alt="Notes App" style="width:50%;">
