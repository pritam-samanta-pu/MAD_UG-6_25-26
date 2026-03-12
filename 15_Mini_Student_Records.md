# Mini Student Records

## Update `pubspec.yaml`

```dart
dependencies:
  flutter:
    sdk: flutter
  sqflite: ^2.3.2
  path: ^1.9.0
```

## `main.dart`

```dart
import 'package:flutter/material.dart';
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

void main() => runApp(const MaterialApp(home: StudentApp()));

// ─── DATABASE ────────────────────────────────────────────
Future<Database> getDB() async => openDatabase(
  join(await getDatabasesPath(), 'students.db'),
  onCreate: (db, _) => db.execute(
    'CREATE TABLE students(id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, address TEXT, contact TEXT)',
  ),
  version: 1,
);

// ─── MAIN SCREEN ─────────────────────────────────────────
class StudentApp extends StatefulWidget {
  const StudentApp({super.key});
  @override
  State<StudentApp> createState() => _State();
}

class _State extends State<StudentApp> {
  final name = TextEditingController();
  final addr = TextEditingController();
  final cont = TextEditingController();
  List<Map> students = [];
  int? editId;

  @override
  void initState() {
    super.initState();
    load();
  }

  Future<void> load() async {
    final db = await getDB();
    final list = await db.query('students');
    setState(() => students = list);
  }

  Future<void> save() async {
    if (name.text.isEmpty) return;
    final db = await getDB();
    final data = {
      'name': name.text,
      'address': addr.text,
      'contact': cont.text,
    };
    editId == null
        ? await db.insert('students', data)
        : await db.update('students', data, where: 'id=?', whereArgs: [editId]);
    name.clear();
    addr.clear();
    cont.clear();
    editId = null;
    load();
  }

  Future<void> delete(int id) async {
    await (await getDB()).delete('students', where: 'id=?', whereArgs: [id]);
    load();
  }

  void edit(Map s) {
    name.text = s['name'];
    addr.text = s['address'];
    cont.text = s['contact'];
    setState(() => editId = s['id']);
  }

  @override
  Widget build(BuildContext context) => Scaffold(
    appBar: AppBar(
      title: const Text('🎓 Student Records'),
      backgroundColor: Colors.indigo,
      foregroundColor: Colors.white,
    ),
    body: Padding(
      padding: const EdgeInsets.all(12),
      child: Column(
        children: [
          // ─ Form ─
          Card(
            child: Padding(
              padding: const EdgeInsets.all(12),
              child: Column(
                children: [
                  TextField(
                    controller: name,
                    decoration: const InputDecoration(
                      labelText: 'Name',
                      prefixIcon: Icon(Icons.person),
                    ),
                  ),
                  TextField(
                    controller: addr,
                    decoration: const InputDecoration(
                      labelText: 'Address',
                      prefixIcon: Icon(Icons.location_on),
                    ),
                  ),
                  TextField(
                    controller: cont,
                    decoration: const InputDecoration(
                      labelText: 'Contact',
                      prefixIcon: Icon(Icons.phone),
                    ),
                  ),
                  const SizedBox(height: 10),
                  SizedBox(
                    width: double.infinity,
                    child: ElevatedButton.icon(
                      onPressed: save,
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.indigo,
                        foregroundColor: Colors.white,
                      ),
                      icon: Icon(editId == null ? Icons.add : Icons.save),
                      label: Text(
                        editId == null ? 'Add Student' : 'Update Student',
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
          const SizedBox(height: 10),
          // ─ List ─
          Expanded(
            child: students.isEmpty
                ? const Center(
                    child: Text(
                      'No students yet.',
                      style: TextStyle(color: Colors.grey),
                    ),
                  )
                : ListView.builder(
                    itemCount: students.length,
                    itemBuilder: (_, i) {
                      final s = students[i];
                      return Card(
                        child: ListTile(
                          leading: CircleAvatar(
                            backgroundColor: Colors.indigo,
                            child: Text(
                              s['name'][0],
                              style: const TextStyle(color: Colors.white),
                            ),
                          ),
                          title: Text(
                            s['name'],
                            style: const TextStyle(fontWeight: FontWeight.bold),
                          ),
                          subtitle: Text('${s['address']} • ${s['contact']}'),
                          trailing: Row(
                            mainAxisSize: MainAxisSize.min,
                            children: [
                              IconButton(
                                icon: const Icon(
                                  Icons.edit,
                                  color: Colors.indigo,
                                ),
                                onPressed: () => edit(s),
                              ),
                              IconButton(
                                icon: const Icon(
                                  Icons.delete,
                                  color: Colors.red,
                                ),
                                onPressed: () => delete(s['id']),
                              ),
                            ],
                          ),
                        ),
                      );
                    },
                  ),
          ),
        ],
      ),
    ),
  );
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/15.png" alt="Mini Student Records" style="width:50%;">
