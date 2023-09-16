# Function

> ## Hide Text
> - img
> - need to pass String 
> - Frist time this func hide 5 characters .If you need to change give int value 
``` dart
    String hideCharacters(String input, {int numToHide = 5}) {
    if (numToHide >= input.length) {
        return "*" * input.length;
    }
    String hiddenPart = "*" * numToHide;
    String visiblePart = input.substring(0, input.length - numToHide - 2);
    String visiblePart2 =
        input.substring(hiddenPart.length + visiblePart.length, input.length);

    return visiblePart + hiddenPart + visiblePart2;
    }
```


> ## Date Time Formater
> - need to pass DateTime 
> - return it String
```dart
    String formatDateTime(DateTime dateTime) {
      // Extract the day, month, and year components from the DateTime object
      int day = dateTime.day;
      int month = dateTime.month;
      int year = dateTime.year;

      // Create a formatted string in "dd/mm/yyyy" format
      String formattedDate = '$day/${month.toString().padLeft(2, '0')}/$year';

      return formattedDate;
    }

```


> ## Countdown Timer
> - img
> - need to pass Future time 
> - The function returns the amount of time left until the target time
``` dart
  String getTimeDifference(DateTime target) {
    Duration difference = target.difference(DateTime.now());
    if (difference.isNegative) {
      return 'Time has passed';
    }
    int days = difference.inDays;
    int hours = difference.inHours.remainder(24);
    int minutes = difference.inMinutes.remainder(60);
    int seconds = difference.inSeconds.remainder(60);

    return '${days}d | ${hours}h | ${minutes}m | ${seconds}s';
  }
```

> ## Countdown Timer 2 (For TextFiled)
> - img
> - need to pass Future time  
> - The function returns the amount of time left until the target time
``` dart
  String getTimeDifference(DateTime target) {
      Duration difference = target.difference(DateTime.now());
      if (difference.isNegative) {
        return '0s';
      }
      int days = difference.inDays;
      int hours = difference.inHours.remainder(24);
      int minutes = difference.inMinutes.remainder(60);
      int seconds = difference.inSeconds.remainder(60);
      if (seconds == 0 && minutes == 0 && hours == 0 && days == 0) {
        return '0s';
      } else if (minutes == 0 && hours == 0 && days == 0) {
        return '${seconds}s';
      } else if (hours == 0 && days == 0) {
        return '${minutes}m ${seconds}s';
      } else if (days == 0) {
        return ' ${hours}h ${minutes}m ${seconds}s';
      }

      return '${days}d ${hours}h ${minutes}m ${seconds}s';
  }
```

> ## M B count
> - img

``` dart
  String formatLargeNumber(double number) {
    if (number >= 1000000000) {
      // Billion (B) abbreviation
      return (number / 1000000000).toStringAsFixed(2) + 'B';
    } else if (number >= 1000000) {
      // Million (M) abbreviation
      return (number / 1000000).toStringAsFixed(2) + 'M';
    } else {
      return number.toStringAsFixed(2); // No abbreviation needed
    }
  }
  
```

> ## Dialog
> - img

``` dart
class PopupDialog {
  // base dialog
  static dynamic base({
    required Widget child,
    BuildContext? context,
    double? width,
    double? borderRadius,
    Color? barrierColor,
    Color?shadowColor,
    double? elevation,
    EdgeInsets? padding
    }) {
    return showDialog<void>(
      // Context
      context:context?? kGlobContext,
      barrierDismissible: false,
      builder: (BuildContext context) {
        return Column(
          // for horizontal minHeight
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            // for ertical minWidth
            Center(
              child: SizedBox(
                // dialog width
                width:width?? 380.w,
                child:Material(
                  elevation:elevation?? 2,
                  // dialog color
                  shadowColor:shadowColor??Colors.black12,
                  // backgraund color
                  color: kWhite,
                  // border radius
                  borderRadius:BorderRadius.circular(borderRadius??12) ,
                  // main body
                  child: Padding(
                    // padding
                    padding:padding?? EdgeInsets.zero,
                    child: child,
                  )),
              ),
            ),
          ],
        );
      },
    );
  }
}
  
```

> ## Custom SnackBar
> - Global context

``` dart
class NavigationService {
  static final navigatorKey = GlobalKey<NavigatorState>();
}

```
> - SnackBar
``` dart
class MySnackBar {
  BuildContext? context;

  MySnackBar({this.context});

  void show(String message, {int duration = 3}) {
    final context =
        this.context ?? NavigationService.navigatorKey.currentContext!;

    SnackBar snackBar = SnackBar(
      backgroundColor: kTextColor,
      content: Text(message,style: const TextStyle(
        color: kWhite,
        fontSize: 16,
        fontWeight: FontWeight.w500
      ),),
      duration: Duration(seconds: duration),
    );
    ScaffoldMessenger.of(context).showSnackBar(snackBar);
  }
}

```









