# Prime Number Finder

## `main.dart`

```dart
import 'package:flutter/material.dart';
import 'package:awesome_notifications/awesome_notifications.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await AwesomeNotifications().initialize(
    null,
    [
      NotificationChannel(
        channelKey: 'basic_channel',
        channelName: 'Basic Channel',
        channelDescription: 'Prime Finder Notifications',
        importance: NotificationImportance.High,
      ),
    ],
  );

  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: PrimePage());
  }
}

class PrimePage extends StatefulWidget {
  const PrimePage({super.key});
  @override
  State<PrimePage> createState() => _PrimePageState();
}

class _PrimePageState extends State<PrimePage> {
  final lowerController = TextEditingController();
  final upperController = TextEditingController();

  List<int> primes = [];
  bool loading = false;

  @override
  void initState() {
    super.initState();
    requestPermission();
  }

  void requestPermission() async {
    bool allowed = await AwesomeNotifications().isNotificationAllowed();
    if (!allowed) {
      await AwesomeNotifications().requestPermissionToSendNotifications();
    }
  }

  // Check prime number
  bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++) {
      if (n % i == 0) return false;
    }
    return true;
  }

  Future<void> findPrimes() async {
    int low = int.parse(lowerController.text);
    int high = int.parse(upperController.text);

    setState(() {
      loading = true;
      primes.clear();
    });

    await Future.delayed(Duration(milliseconds: 100));

    List<int> result = [];

    for (int i = low; i <= high; i++) {
      if (isPrime(i)) {
        result.add(i);
      }
    }

    setState(() {
      primes = result;
      loading = false;
    });

    await AwesomeNotifications().createNotification(
      content: NotificationContent(
        id: 1,
        channelKey: 'basic_channel',
        title: 'Prime Finder',
        body: 'Prime number calculation completed!',
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Prime Number Finder")),
      body: Padding(
        padding: const EdgeInsets.all(16),
        child: Column(
          children: [
            SizedBox(height: 90,),
            TextField(
              controller: lowerController,
              keyboardType: TextInputType.number,
              decoration: InputDecoration(labelText: "Lower Range"),
            ),
            TextField(
              controller: upperController,
              keyboardType: TextInputType.number,
              decoration: InputDecoration(labelText: "Upper Range"),
            ),
            SizedBox(height: 20),

            ElevatedButton(
              onPressed: findPrimes,
              child: Text("Find Primes"),
            ),

            SizedBox(height: 20),

            if (loading) CircularProgressIndicator(),

            Expanded(
              child: ListView.builder(
                itemCount: primes.length,
                itemBuilder: (context, index) {
                  return ListTile(
                    title: Text(primes[index].toString()),
                  );
                },
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

<img src="https://github.com/pritam-samanta-pu/MAD_UG-6_25-26/blob/main/Output/8.png" alt="Prime Number Finder" style="width:50%;">
