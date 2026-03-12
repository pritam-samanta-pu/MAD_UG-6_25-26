# Dark Mode Toggle

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
import 'package:shared_preferences/shared_preferences.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  final prefs = await SharedPreferences.getInstance();
  final isDark = prefs.getBool('darkMode') ?? false;
  runApp(MyApp(isDark: isDark));
}

class MyApp extends StatefulWidget {
  final bool isDark;
  const MyApp({super.key, required this.isDark});
  @override
  State<MyApp> createState() => MyAppState();
}

class MyAppState extends State<MyApp> {
  late bool isDark;

  @override
  void initState() {
    super.initState();
    isDark = widget.isDark;
  }

  Future<void> toggleTheme(bool value) async {
    final prefs = await SharedPreferences.getInstance();
    await prefs.setBool('darkMode', value);
    setState(() => isDark = value);
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      themeMode: isDark ? ThemeMode.dark : ThemeMode.light,
      theme: ThemeData.light(useMaterial3: true),
      darkTheme: ThemeData.dark(useMaterial3: true),
      home: HomeScreen(isDark: isDark, onToggle: toggleTheme),
    );
  }
}

class HomeScreen extends StatelessWidget {
  final bool isDark;
  final ValueChanged<bool> onToggle;
  const HomeScreen({super.key, required this.isDark, required this.onToggle});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Dark Mode Toggle')),
      body: Center(
        child: Card(
          margin: const EdgeInsets.all(24),
          elevation: 4,
          child: Padding(
            padding: const EdgeInsets.all(24),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                Icon(
                  isDark ? Icons.dark_mode : Icons.light_mode,
                  size: 64,
                  color: isDark ? Colors.amber : Colors.orange,
                ),
                const SizedBox(height: 16),
                Text(
                  isDark ? 'Dark Mode ON' : 'Light Mode ON',
                  style: const TextStyle(
                    fontSize: 20,
                    fontWeight: FontWeight.bold,
                  ),
                ),
                const SizedBox(height: 8),
                Text(
                  'Your preference is saved!',
                  style: TextStyle(color: Colors.grey[600]),
                ),
                const SizedBox(height: 20),
                Switch(
                  value: isDark,
                  onChanged: onToggle,
                  thumbIcon: WidgetStateProperty.resolveWith((states) {
                    return Icon(
                      states.contains(WidgetState.selected)
                          ? Icons.dark_mode
                          : Icons.light_mode,
                      size: 16,
                    );
                  }),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

## Output

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/14.png" alt="Dark Mode Toggle" style="width:50%;">
<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/14a.png" alt="Dark Mode Toggle" style="width:50%;">
