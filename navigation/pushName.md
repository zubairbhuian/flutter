## PushName


> - Make a route in *MaterialApp*
> - The initialRoute must have to 




```dart
      initialRoute: "/",
      routes: {
        "/first": (context) => const FristScreen(),
        "/second": (context) => const SecondScreen()
      }

```

> Make the Route

```dart
        Navigator.pushNamed(context, "/first");
```