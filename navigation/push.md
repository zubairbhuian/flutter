## Push Navigation

> There is a simple *push* structure
```dart
 Navigator.push(context,MaterialPageRoute(builder: (context) =>FristScreen()))
```

> ## Full Code
```dart
    import 'package:flutter/material.dart';

    void main() => runApp(MyApp());

    class MyApp extends StatelessWidget {
    const MyApp({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return MaterialApp(
        debugShowCheckedModeBanner: false,
        theme: ThemeData(primarySwatch: Colors.pink),
        home: const SafeArea(child: FristScreen()),
        );
    }
    }

    class FristScreen extends StatefulWidget {
    const FristScreen({Key? key}) : super(key: key);

    @override
    State<FristScreen> createState() => _FristScreenState();
    }

    class _FristScreenState extends State<FristScreen> {
    @override
    Widget build(BuildContext context) {
        return Scaffold(
        body: Center(
            child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
                Container(
                color: Colors.red,
                height: 50,
                child: const Center(
                    child: Text(
                    "This is Frist Page",
                    style: TextStyle(color: Colors.white, fontSize: 22),
                )),
                ),
                OutlinedButton(
                    onPressed: () {
                    Navigator.push(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const SecondScreen()));
                    },
                    child: Text("Second Screen")),
            ],
            ),
        ),
        );
    }
    }

    class SecondScreen extends StatefulWidget {
    const SecondScreen({Key? key}) : super(key: key);

    @override
    State<SecondScreen> createState() => _SecondScreenState();
    }

    class _SecondScreenState extends State<SecondScreen> {
    @override
    Widget build(BuildContext context) {
        return Scaffold(
        body: Center(
            child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
                Container(
                color: Colors.red,
                height: 50,
                child: const Center(
                    child: Text(
                    "This is Seconed Page",
                    style: TextStyle(color: Colors.white, fontSize: 22),
                )),
                ),
                OutlinedButton(
                    onPressed: () {
                    Navigator.push(
                        context,
                        MaterialPageRoute(
                            builder: (context) => const FristScreen()));
                    },
                    child: const Text("Frist Screen")),
            ],
            ),
        ),
        );
    }
    }

```