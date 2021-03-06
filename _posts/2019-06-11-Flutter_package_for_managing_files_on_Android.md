---
layout: post
title:  Android 文件管理器
tag: [File Manager]
date: 2019-06-11
---

 


## [立即下载 ️⬇️ ](https://codeload.github.com/Eagle6789/flutter_file_manager/zip/master) 


 
![](https://flutterawesome.com/content/images/2019/05/flutter_file_manager.jpg)
 
>
> 
>

 
# flutter_file_manager

[![pub package](https://img.shields.io/pub/v/flutter_file_manager.svg)](https://pub.dartlang.org/packages/flutter_file_manager)

A set of utilities, that help to manage the files & directories in Android system.

You are in your way to create File Manager app or a Gallery App.

## Getting Started

For help getting started with Flutter, view our online [documentation](https://flutter.io/).

For help on editing package code, view the [documentation](https://flutter.io/developing-packages/).

## Screenshots

<p>
  <img src="https://github.com/Eagle6789/flutter_file_manager/blob/master/screenshots/ss1.png?raw=true" height="300em" /> <img src="https://github.com/Eagle6789/flutter_file_manager/raw/master/screenshots/ss2.jpg" height="300em"/>
  <img src="https://github.com/Eagle6789/flutter_file_manager/raw/master/screenshots/ss3.jpg" height="300em" /> <img src="https://github.com/Eagle6789/flutter_file_manager/raw/master/screenshots/ss4.jpg" height="300em"/>
  <img src="https://github.com/Eagle6789/flutter_file_manager/raw/master/screenshots/ss5.jpg" height="300em" /> <img src="https://github.com/Eagle6789/flutter_file_manager/raw/master/screenshots/ss6.jpg" height="300em" /> <img src="https://github.com/Eagle6789/flutter_file_manager/raw/master/screenshots/ss7.jpg" height="300em" />
</p>

## Usage

To use this package, add these  
dependency in your `pubspec.yaml`  file.

```yaml
dependencies:
  flutter:
    sdk: flutter
  path: 1.6.2
  path_provider: 0.5.0+1
  flutter_file_manager: ^0.1.1
```

And, add read / write permissions in your
`android/app/src/main/AndroidManifest.xml`

````xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
````

Don't forget to grant `Storage` permissions to your app, manually or by this plugin [simple_permissions](https://pub.dartlang.org/packages/simple_permissions)

```dart
// framework
import 'package:flutter/material.dart';

// packages
import 'package:flutter_file_manager/flutter_file_manager.dart';
import 'package:path_provider/path_provider.dart';
import 'package:path/path.dart' as p;

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: Scaffold(
          appBar: AppBar(
            title: Text("Flutter File Manager Demo"),
          ),
          body: FutureBuilder(
            future: _files(), // a previously-obtained Future<String> or null
            builder: (BuildContext context, AsyncSnapshot snapshot) {
              switch (snapshot.connectionState) {
                case ConnectionState.none:
                  return Text('Press button to start.');
                case ConnectionState.active:
                case ConnectionState.waiting:
                  return Text('Awaiting result...');
                case ConnectionState.done:
                  if (snapshot.hasError)
                    return Text('Error: ${snapshot.error}');
                  return snapshot.data != null
                      ? ListView.builder(
                          itemCount: snapshot.data.length,
                          itemBuilder: (context, index) => Card(
                                  child: ListTile(
                                title: Text(snapshot.data[index].absolute.path),
                                subtitle: Text(
                                    "Extension: ${p.extension(snapshot.data[index].absolute.path).replaceFirst('.', '')}"), // getting extension
                              )))
                      : Center(
                          child: Text("Nothing!"),
                        );
              }
              return null; // unreachable
            },
          )),
    );
  }

  _files() async {
    var root = await getExternalStorageDirectory();
    var fm = FileManager(root: root);
    var files = await fm.filesTree(excludedPaths: ["/storage/emulated/0/Android"]);
    return files;
  }
}
```

### Example

* [examples](https://github.com/Eagle6789/flutter_file_manager/tree/master/example/lib)

### Features

* file details
* search files or directories: supports regular expressions
* recent created files: you can exclude a list of directories from the tree 
* directories only tree: you can exclude a list of directories from the tree
* files only tree: you can exclude a list of directories from the tree
* files list from specific point
* delete files
* delete directory
* temp file
* Sorting file by: type, size, date, ..

### Contributors

* [Mohamed Naga](https://github.com/eagle6789)

## Feel free to donate

* [PayPal](https://www.paypal.me/eagle6789)
* me49544@gmail.com

### Contact me

* me.developer.a@gmail.com

## Github主页 👉[Eagle6789/flutter_file_manager](http://github.com/Eagle6789/flutter_file_manager)