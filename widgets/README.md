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
class CustomDropdownTextField extends StatelessWidget {
  const CustomDropdownTextField(
      {super.key,
      this.label,
      required this.data,
      required this.onChanged,
      this.hint, this.marginBottom});

  final String? label;
  final double? marginBottom;
  final List data;
  final Widget? hint;
  final Function(String?) onChanged;

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
         // label text
        if (label != null)
          Text(
            label ?? '',
            style: kTitleSmall(),
          ),
        // gapping
        SizedBox(height: label == null ? 0 : 8),
        DropdownButtonFormField<String>(
          //hint Style
          hint: hint ??
              Text(
                'Admin',
                style: kTitleSmall()?.copyWith(color: kTextColorLite),
              ),
          // arrow icon
          // icon: SvgPicture.asset('assets/icons/arrow-down.svg'),
          dropdownColor: kWhite,
          decoration: InputDecoration(
              // padding
              contentPadding:
                  const EdgeInsets.symmetric(vertical: 18, horizontal: 20),
              // border 
              border: InputBorder.none,
              focusedBorder: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(8),
                  borderSide: const BorderSide(color: kTextColor)),
              enabledBorder: OutlineInputBorder(
                  borderRadius: BorderRadius.circular(8.r),
                  borderSide: const BorderSide(color: kTextColor)),
              // filled color 
              filled: true,
              // Set the background color here
              fillColor: kWhite,
              ),
          // generate select items
          items: List.generate(
              data.length,
              (index) => DropdownMenuItem<String>(
                    value: data[index],
                    child: Text(
                      data[index],
                      style: kTitleSmall()?.copyWith(color: kTextColor),
                    ),
                  )),
          onChanged: onChanged,
        ),
        // bottom gap
        SizedBox(height:marginBottom?? 16),
      ],
    );
  }
}


```



> ## DotContainer
``` dart
import 'package:flutter/material.dart';

// +++++++ dot widgets ++++++++
class DotContainer extends StatelessWidget {
  final Widget child;
  final double? borderRadius;
  final Color? dotColor;
  final double? dotWidth;
  final double? dotheith;
  final double? dotgap;
  final Color? color;
  final EdgeInsetsGeometry? padding;
  final EdgeInsetsGeometry? margin;
  final StrokeCap? dotShape;
  const DotContainer({
    Key? key,
    this.dotShape,
    required this.child,
    this.borderRadius,
    this.dotColor,
    this.dotWidth,
    this.dotheith,
    this.dotgap,
    this.color,
    this.padding,
    this.margin,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: margin,
      decoration: BoxDecoration(
          color: color,
          borderRadius: BorderRadius.circular(borderRadius ?? 12)),
      child: Stack(
        children: [
          Container(
            padding: padding,
            decoration: BoxDecoration(
                borderRadius: BorderRadius.circular(borderRadius ?? 12)),
            child: child,
          ),
          Positioned(
            left: 0,
            right: 0,
            top: 0,
            bottom: 0,
            child: SizedBox(
                child: CustomPaint(
              painter: _DottedBorderPainter(
                  dotShape: StrokeCap.round,
                  borderRadius: borderRadius ?? 4,
                  color: dotColor ?? Colors.black,
                  dotWidth: dotWidth ?? 1,
                  dotheith: dotheith ?? 2,
                  dotgap: dotgap ?? 2),
            )),
          ),
        ],
      ),
    );
  }
}

// ++++++ Genarate dot posint ++++++++
class _DottedBorderPainter extends CustomPainter {
  final double borderRadius;
  final Color color;
  final double dotWidth;
  final double dotheith;
  final double dotgap;
  final StrokeCap dotShape;

  _DottedBorderPainter(
      {required this.dotShape,
      required this.borderRadius,
      required this.color,
      required this.dotWidth,
      required this.dotheith,
      required this.dotgap});

  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()
      // dotColor
      ..color = color
      // dot width
      ..strokeWidth = dotWidth
      // dot style
      ..style = PaintingStyle.stroke
      // dot shape
      ..strokeCap = dotShape;

    final path = Path()
      ..addRRect(RRect.fromRectAndRadius(
          Offset.zero & size, Radius.circular(borderRadius)));
    canvas.drawPath(
      // dot width & height
      dashPath(path, dashWidth: dotheith, dashSpace: dotgap),
      paint,
    );
  }

  @override
  bool shouldRepaint(CustomPainter oldDelegate) {
    return false;
  }

  @override
  bool shouldRebuildSemantics(_DottedBorderPainter oldDelegate) {
    return false;
  }
}

// ++++++++ dot path ++++++++++++
Path dashPath(Path path, {double dashWidth = 3.0, double dashSpace = 2.0}) {
  final metrics = path.computeMetrics();
  final dashPath = Path();

  for (final metric in metrics) {
    double distance = 0;
    while (distance < metric.length) {
      dashPath.addPath(
        metric.extractPath(distance, distance + dashWidth),
        Offset.zero,
      );
      distance += dashWidth + dashSpace;
    }
  }

  return dashPath;
}



```

