# Widgets

> ## Button 
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

> ## TextField
``` dart
    class CustomTextField extends StatefulWidget {
    final TextEditingController? controller;
    final bool? obscureText;
    final bool? readOnly;
    final Widget? suffixIcon;
    final Widget? prefixIcon;
    final String? hintText;
    final Widget? label;
    final VoidCallback? onTap;
    final AutovalidateMode? autovalidateMode;
    final TextInputType? keyboardType;
    final String? Function(String?)? validator;
    final Function(String)? onChange;
    final EdgeInsetsGeometry? padding;
    final Color? borderColor;
    final Color? focusedBorderColor;
    final Color? enabledBorderColor;
    final Color? cursorColor;
    final TextAlign? textAlign;
    final double? fontSize;
    final List<TextInputFormatter>? inputFormatters;
    final bool? autofocus;
    final double? borderRadius;
    final FontWeight? hintFontWeight;
    final Color? hintColor;
    final TextStyle? style;
    final String? errorText;
    final VoidCallback? onEditingComplete;
    final EdgeInsetsGeometry? margin;
    final double? marginBottom;
    final int? maxLines;

    const CustomTextField(
        {super.key,
        this.controller,
        this.obscureText,
        this.readOnly,
        this.suffixIcon,
        this.prefixIcon,
        this.hintText,
        this.label,
        this.onTap,
        this.autovalidateMode,
        this.keyboardType,
        this.validator,
        this.onChange,
        this.padding,
        this.borderColor,
        this.focusedBorderColor,
        this.enabledBorderColor,
        this.cursorColor,
        this.inputFormatters,
        this.autofocus,
        this.textAlign,
        this.fontSize,
        this.borderRadius,
        this.hintFontWeight,
        this.hintColor,
        this.style,
        this.errorText,
        this.onEditingComplete,
        this.margin,
        this.marginBottom,
        this.maxLines});

    @override
    State<CustomTextField> createState() => _CustomTextFieldState();
    }

    class _CustomTextFieldState extends State<CustomTextField> {
    FocusNode _focusNode = FocusNode();
    bool _isFocused = false;

    @override
    void initState() {
        super.initState();
        _focusNode.addListener(_onFocusChange);
    }

    @override
    void dispose() {
        _focusNode.removeListener(_onFocusChange);
        _focusNode.dispose();
        super.dispose();
    }

    void _onFocusChange() {
        setState(() {
        _isFocused = _focusNode.hasFocus;
        });
    }

    @override
    Widget build(BuildContext context) => Container(
            margin: widget.margin ??
                EdgeInsets.only(
                    left: 30, right: 30, bottom: widget.marginBottom ?? 20),
            decoration: ShapeDecoration(
            color: Colors.black,
            shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
            shadows: _isFocused ? [] : inputShadow,
            ),
            child: TextFormField(
            controller: widget.controller,
            validator: widget.validator,
            focusNode: _focusNode,
            onChanged: widget.onChange,
            obscureText: widget.obscureText ?? false,
            readOnly: widget.readOnly ?? false,
            autovalidateMode: widget.autovalidateMode,
            cursorColor: widget.cursorColor,
            maxLines: widget.maxLines ?? 1,
            autofocus: widget.autofocus ?? false,
            textAlign: widget.textAlign ?? TextAlign.start,
            onTap: widget.onTap,
            style: widget.style ??
                TextStyle(
                    color: Colors.white,
                    fontSize: 16,
                    fontFamily: 'Poppins',
                    fontWeight: FontWeight.w400,
                    height: 1.50,
                    letterSpacing: 0.15,
                ),
            onEditingComplete: widget.onEditingComplete,
            keyboardType: widget.keyboardType,
            decoration: InputDecoration(
                errorText: widget.errorText,
                contentPadding: widget.padding ??
                    EdgeInsets.symmetric(vertical: 18, horizontal: 20),
                prefixIcon: widget.prefixIcon,
                suffixIcon: widget.suffixIcon,
                border: InputBorder.none,
                focusedBorder: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(widget.borderRadius ?? 8),
                    borderSide: BorderSide(
                        width: 1,
                        color: widget.focusedBorderColor ?? Colors.white)),
                enabledBorder: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(widget.borderRadius ?? 8),
                    borderSide: BorderSide(
                        width: 1,
                        color: widget.enabledBorderColor ?? Colors.transparent)),
                errorBorder: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(widget.borderRadius ?? 8),
                    borderSide: BorderSide(
                        width: 1, color: widget.enabledBorderColor ?? Colors.red)),
                hintText: widget.hintText,
                label: widget.label,
                hintStyle: TextStyle(
                color: Color(0xFFC0C0C0),
                fontSize: 16,
                fontFamily: 'Poppins',
                fontWeight: FontWeight.w400,
                letterSpacing: 0.15,
                ),
            ),
            inputFormatters:
                widget.inputFormatters ?? [LengthLimitingTextInputFormatter(40)],
            ),
        );
    }
```

> ## Selected TextField
> - need to pass a List<String>  
``` dart
    class CustomDropdownTextFiel extends StatefulWidget {
    const CustomDropdownTextFiel(
        {super.key,
        required this.label,
        required this.data,
        required this.onChanged,
        this.hint});

    final String label;
    final List data;
    final Widget? hint;
    final Function(String?) onChanged;

    @override
    State<CustomDropdownTextFiel> createState() => _CustomDropdownTextFielState();
    }

    class _CustomDropdownTextFielState extends State<CustomDropdownTextFiel> {
    FocusNode _focusNode = FocusNode();
    bool _isFocused = false;

    @override
    void initState() {
        super.initState();
        _focusNode.addListener(_onFocusChange);
    }

    @override
    void dispose() {
        _focusNode.removeListener(_onFocusChange);
        _focusNode.dispose();
        super.dispose();
    }

    void _onFocusChange() {
        setState(() {
        _isFocused = _focusNode.hasFocus;
        });
    }

    @override
    Widget build(BuildContext context) {
        return Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
            Text(
            widget.label,
            style: TextStyle(
                fontSize: 14.sp,
                color: Color.fromARGB(255, 255, 255, 255),
            ),
            ),
            SizedBox(height: 8.h),
            Container(
            decoration: ShapeDecoration(
                color: Colors.black,
                shape:
                    RoundedRectangleBorder(borderRadius: BorderRadius.circular(8)),
                shadows: _isFocused ? [] : inputShadow,
            ),
            child: DropdownButtonFormField<String>(
                hint: widget.hint ??
                    Text(
                    'Select',
                    style: TextStyle(
                        color: Color(0xFFC0C0C0),
                        fontSize: 16,
                        fontFamily: 'Poppins',
                        fontWeight: FontWeight.w400,
                        letterSpacing: 0.15,
                    ),
                    ),
                icon: SvgPicture.asset('assets/icons/arrow-down.svg'),
                dropdownColor: Colors.black,
                decoration: InputDecoration(
                    contentPadding:
                        EdgeInsets.symmetric(vertical: 18, horizontal: 20),
                    border: InputBorder.none,
                    focusedBorder: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8),
                        borderSide: const BorderSide(color: Colors.white)),
                    enabledBorder: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8.r),
                        borderSide: const BorderSide(color: Colors.black)),
                    filled: true,
                    fillColor: Colors.black,
                    hintStyle: TextStyle(
                        color: Colors.black,
                        fontSize: 16.sp) // Set the background color here
                    ),
                items: List.generate(
                    widget.data.length,
                    (index) => DropdownMenuItem<String>(
                        value: widget.data[index],
                        child: Text(
                            widget.data[index],
                            style: TextStyle(
                            color: Colors.white,
                            fontSize: 16,
                            fontFamily: 'Poppins',
                            fontWeight: FontWeight.w400,
                            height: 1.50,
                            letterSpacing: 0.15,
                            ),
                        ),
                        )),
                onChanged: widget.onChanged,
            ),
            ),
            SizedBox(height: 24.h),
        ],
        );
    }
    }


```