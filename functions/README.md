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


