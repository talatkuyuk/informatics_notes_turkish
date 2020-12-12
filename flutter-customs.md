

### Custom TextStyle
```dart
class UITextStyles {
  static TextStyle loginStyle = TextStyle(
      fontFamily: 'Montserrat',
      color: UIHelper.WHITE,
      fontSize: 45,
      fontWeight: FontWeight.w500);
}
Text("login", style: UITextStyles.loginStyle); //Bu şekilde kullanabilirsiniz.
```

### Custom BoxDecoration
```dart
class UIBoxDecoration {
static BoxDecoration boxStyle = BoxDecoration(
      boxShadow: [
        BoxShadow(
            color: Colors.blue,
            blurRadius: 10.0,
            spreadRadius: 1.0,
            offset: Offset(
              3.0,
              3.0,
            )),
      ],
      borderRadius: BorderRadius.only(
          bottomLeft: Radius.circular(UIHelper.dynamicWidth(150)),
          bottomRight: Radius.circular(UIHelper.dynamicWidth(150))),
      color: Colors.blue);
}
decoration: UIBoxDecoration.boxStyle, //Bu şekilde kullanabilirsiniz.
```

### Custom BorderRadius
```dart
BorderRadius get _loginButtonBorderStyle => BorderRadius.only(
      bottomRight: Radius.circular(80),
      topRight: Radius.circular(80),
    );
// Bu şekilde kullanabilirsiniz.
BoxDecoration(color: Colors.white, borderRadius: _loginButtonBorderStyle),
```

### Custom Widgets
```dart
//Kullanım: _loginButton
Widget get _loginButton => InkWell(
    borderRadius: _loginButtonBorderStyle,
    onTap: () {},
    child: Container(
      height: UIHelper.dynamicHeight(300),
      width: UIHelper.dynamicWidth(500),
      child: Center(
        child: Text(UIHelper.signIn.toUpperCase(),
            style: UITextStyles.buttonStyle),
      ),
    ),
);

// Kullanım: _textField("Username", true)
Widget _textField(String text, bool obscure) => TextField(
    style: TextStyle(color: Colors.white),
    textAlign: TextAlign.left,
    obscureText: obscure,
    autocorrect: false,
    cursorColor: Colors.white,
    maxLines: 1,
);
```

### Custom Theme
```dart
final ThemeData theme = ThemeData(
    primaryColor: Colors.blue,
    accentColor: Colors.blueAccent,
    textTheme: TextTheme(body1: TextStyle(color: Colors.lightBlue))
  );
```

### Custom Helpers
```dart
class UITextHelper {
  static final String name = "Name";
  static final String email = "Email address";
  static final String username = "Username";
  static final String password = "Password";
  static final String login = "Login";
  static final String forgetPassword = "Forget Password?";
}
UITextHelper.DEGISKEN_ADI // kullanım

class UIColorHelper {
  static const Color PRIMARY_COLOR = Color(0xFF1A237E);
  static const Color LIGHT_COLOR = Color(0xFF534BAE);
  static const Color DARK_COLOR = Color(0xFF000051);
  static const Color TEXT_COLOR = Color(0xFFFFFFFF);
}
UIColorHelper.DEGISKEN_ADI // kullanım
```