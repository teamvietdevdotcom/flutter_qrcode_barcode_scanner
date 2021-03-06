# Flutter QR Code & Barcode Scanner

Hướng dẫn xây dựng ứng dụng Flutter với các tính năng quét mã QR Code và Barcode (QR Code & Barcode Scanner).

Sau đây là giao diện mẫu quét mã QR Code và Barcode (QR Code & Barcode Scanner) bằng Flutter bạn có thể tham khảo:

<img src="https://teamvietdev.com/wp-content/uploads/2018/11/teamvietdev-quet-ma-qr-code-va-barcode-trong-flutter-vi-du-768x444.jpg" alt="QR Code & Barcode Scanner bằng Flutter">

Mã nguồn <a href="https://teamvietdev.com/quet-ma-qr-code-va-barcode-trong-flutter/">QR Code & Barcode Scanner trong Flutter</a>:

```
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';
import 'package:barcode_scan/barcode_scan.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'QR Code & Barcode Scanner',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'QR Code & Barcode Scanner'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

  String result = "Please scan the QR code or Barcode";

  Future _scanQR() async {
    try {
      String qrResult = await BarcodeScanner.scan();
      setState(() {
        result = qrResult;
      });
    } on PlatformException catch (ex) {
      if (ex.code == BarcodeScanner.CameraAccessDenied) {
        setState(() {
          result = "Camera permission was denied";
        });
      } else {
        setState(() {
          result = "Unknown Error $ex";
        });
      }
    } on FormatException {
      setState(() {
        result = "You pressed the back button before scanning anything";
      });
    } catch (ex) {
      setState(() {
        result = "Unknown Error $ex";
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("QR Code & Barcode Scanner"),
      ),
      body: Center(
        child: Text(
          result,
          style: new TextStyle(fontSize: 20.0, fontWeight: FontWeight.bold),
        ),
      ),
      floatingActionButton: FloatingActionButton.extended(
        icon: Icon(Icons.camera_alt),
        label: Text("Scan"),
        onPressed: _scanQR,
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerFloat,
    );
  }
}
```

Tìm hiểu thêm về <a href="https://teamvietdev.com/chuyen-muc/flutter/">Flutter</a> tại 
<a href="https://teamvietdev.com/">Team Việt Dev</a>.
