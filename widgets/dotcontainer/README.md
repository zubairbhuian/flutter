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
    return Stack(
      children: [
        Container(
          padding: padding,
          margin: margin,
          decoration: BoxDecoration(
              color: color,
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
                color: color ?? Colors.black,
                dotWidth: dotWidth ?? 1,
                dotheith: dotheith ?? 2,
                dotgap: dotgap ?? 2),
          )),
        ),
      ],
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