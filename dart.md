## Dart Notları


### Snackbar 
```dart
final _scaffoldKey = GlobalKey<ScaffoldState>();

final snackBar = SnackBar(content: Text('Are you talking to me?'));
_scaffoldKey.currentState.showSnackBar(snackbar); 
```

### Veri Tanımlama Çeşitleri
```dart
  // List<String>
  var messages = const [
    "a", "b", "c", "d"
  ];

  // List<Map>  //Map phthon'da Dictionary yapısı ile aynıdır. key-value
  // List<Map<String, String>> 
  var structuredMessages = const [
    {"subject": "Title 1",
     "body": "dkd kdjlkdfj dflkjglkdjfg dslkfjglkjdfg dlfglkdfj dfljdflkgjdklf", 
    },
    {"subject": "Title 2",
     "body": "zxc kdjlkdfj dflkjglkdjfg dslkfjglkjdfg dlfglkdfj dfljdflkgjdklf", 
    },
  ];


EdgeInsets globalMargin =
    const EdgeInsets.symmetric(horizontal: 20.0, vertical: 20.0);

TextStyle textStyle = const TextStyle(
  fontSize: 100.0,
  color: Colors.black,
);
```
