# Flutter Notları


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
> cd C:\MyCodeRepo\flutterprojects
> flutter create --org com.yourdomain appname
```
Bu şekilde yaratırsan en başta hoş olur, sonra değiştirmesi zor oluyor. Örnek kullanım:
```powershell
> flutter create --org com.ipikuka shopping_list
```

Fluuter projede dependency'leri görmek için:
```powershell
> flutter pub deps
```

## Flutter Projesi için SHA-1 keyi tespit etmek
Öncelikle bilgisayarda [Java SE Development Kit 14](https://www.oracle.com/java/technologies/javase-jdk14-downloads.html) kurulu olması gerekiyor.
Windows'ta kurulu bu JDK için Environment Variable'ların olduğunu kontrol edelim, yoksa Kullanıcı için değişkenler bölümüne ekleyelim. (JDK'nın kurulu olduğu klasör ne ise onu dikkate alalım)
> JAVA_HOME olarak C:\Program Files\Java\jdk-14.0.1<br>
> JAVA_BIN olarak C:\Program Files\Java\jdk-14.0.1\bin<br>
> JAVA_LIB olarak C:\Program Files\Java\jdk-14.0.1\lib<br>

"c:\path-to\your-flutter-project-folder\android\gradle\wrapper\gradle-wrapper.properties" dosyasındaki distributionUrl'nin uyumlu gradle olmasını sağlayalım.
> distributionUrl=https\://services.gradle.org/distributions/gradle-6.3-all.zip

Tüm bu ayarlamaları yaptıktan sonra CMD komut satırında flutter projesinin android klasörüne gidelim,
> cd c:\path-to\your-flutter-project-folder\android\ 

Komut satırına aşağıdaki komutu yazalım, bu komut gerekli tüm servisler için SHA-1'leri ve diğer bilgileri ekrana raporlayacaktır.
```powershell
gradlew signingReport
```