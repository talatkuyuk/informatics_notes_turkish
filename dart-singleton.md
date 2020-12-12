# Dart Dilinde Singleton Yapısı
https://stackoverflow.com/questions/54057958/comparing-ways-to-create-singletons-in-dart

###  Singleton with Factory Constructor
```dart
class MyClass {
    static final MyClass _instance = MyClass._internalConstructor();
    
    // opt 1
    factory MyClass() => _instance
    // opt 2
    factory MyClass() {
        return _instance;
    }
    
    // opt 1
    MyClass._internalConstructor();
    // opt 2
    MyClass._internalConstructor() {
        // initialization logic here
    }

    // rest of the class
}

main() {
  // consuming code: getting singleton instance
  MyClass myObj1 = new MyClass(); 

  // another consuming code: still getting singleton instance
  MyClass myObj2 = new MyClass(); 

  print(identical(myObj1, myObj1));  // true
  print(myObj1 == myObj1);  // true
}
```


###  Singleton with Controlled Getter
```dart
class MyClass {
  static MyClass _instance;

  static MyClass get instance {
    if (_instance == null) _instance = MyClass.internal();
    return _instance;
  }
  
  final IconData cancel = Icons.cancel;
  final IconData search = Icons.search;
  final IconData add = Icons.add;
  
  MyClass.internal();
}
```


###  Singleton with Getter
```dart
class MyClass {

  MyClass._internalConstructor();

  static final MyClass _instance = MyClass._internalConstructor();

  static MyClass get instance => _instance;
}
// Instantiation
MyClass service = MyClass.instance;
```



###  Singleton with Static Field
```dart
class Singleton {
  static final Singleton _instance = Singleton._privateConstructor();

  Singleton._privateConstructor();

  static Singleton getInstance() {
    return _instance;
  }
}
// Instantiation
Singleton service = Singleton.getInstance;


class Singleton {

  Singleton._privateConstructor();

  static final Singleton instance = Singleton._privateConstructor();
}
// Instantiation
Singleton service = Singleton.instance;
```


