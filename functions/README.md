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
