## Flutter Notları


## Flutter Kurulumu

Flutter kurulumunu Windows'ta ``C:\flutter`` adlı klasöre yaptım.--
Environment Variables içindeki PATH değişkenine ``C:\flutter\bin`` ekledim.


## Flutter github’daki Flutter Galery Çalıştırmak

Flutter Galery uygulaması, Flutter ile gelen widget'ların örnek kullanımlarını göstermektedir.
Flutter kurulurken %FLUTTER-DIRECTORY%/examples/flutter_gallery altında gelmektedir.

```powershell
> cd C:\flutter\examples\flutter_gallery
> flutter pub get
```

Android phone debug modunda pc’ye bağla
```powershell
> flutter run –release -d <Telephone>
> flutter run –release -d HVY0219223005212
```

## Flutter projesini domain name ile yaratmak
```powershell
cd C:\MyCodeRepo\flutterprojects
flutter create --org com.yourdomain appname
```
Bu şekilde yaratırsan en başta hoş olur, sonra değiştirmesi zor oluyor. Örnek kullanım:
```powershell
flutter create --org com.ipikuka shopping_list
```