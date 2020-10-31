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

Flutter projede dependency'leri görmek için:
```powershell
> flutter pub deps
```

Flutter kanal bilgisini görmek için:
```powershell
> flutter channel
```

Flutter kanalı değiştirmek için: stable, beta, dev, and master
```powershell
> flutter channel <channel-name>
> flutter channel dev
> flutter channel stable
```

To identify out-of-date package dependencies and get advice on how to update them, use the outdated command
```powershell
> flutter pub outdated
```

To update to the latest compatible versions of all the dependencies listed in the pubspec.yaml file
```powershell
> flutter pub upgrade
```

## Flutter Projesi için SHA-1 keyi tespit etmek
Öncelikle bilgisayarda [Java SE Development Kit 14](https://www.oracle.com/java/technologies/javase-jdk14-downloads.html) kurulu olması gerekiyor.
Windows'ta kurulu bu JDK için Environment Variable'ların olduğunu kontrol edelim, yoksa Kullanıcı için değişkenler bölümüne ekleyelim. (JDK'nın kurulu olduğu klasör ne ise onu dikkate alalım)
> JAVA_HOME olarak C:\Program Files\Java\jdk-14.0.1<br>
> JAVA_BIN olarak C:\Program Files\Java\jdk-14.0.1\bin<br>
> JAVA_LIB olarak C:\Program Files\Java\jdk-14.0.1\lib<br>
> PATH değişkenine mevcutlara ilave olarak C:\Program Files\Java\jdk-14.0.1\bin<br>

"c:\path-to\your-flutter-project-folder\android\gradle\wrapper\gradle-wrapper.properties" dosyasındaki distributionUrl'nin uyumlu gradle olmasını sağlayalım.
> distributionUrl=https\://services.gradle.org/distributions/gradle-6.3-all.zip

Tüm bu ayarlamaları yaptıktan sonra CMD komut satırında flutter projesinin android klasörüne gidelim,
```powershell
> cd c:\path-to\your-flutter-project-folder\android\ 
```

Komut satırına aşağıdaki komutu yazalım, bu komut gerekli tüm servisler için SHA-1'leri ve diğer bilgileri ekrana raporlayacaktır.
```powershell
> gradlew signingReport
```

Komut satırına aşağıdaki de yazılırsa SHA-1'i direkt verecektir.
```powershell
> keytool -list -v -alias androiddebugkey -keystore %USERPROFILE%\.android\debug.keystore
```
Release için SHA-1 ise, android studio'da jks dosyası oluşturuluyor, sonra komut satırında,
```powershell
> keytool -exportcert -list -v -alias <your-key-name> -keystore <path-to-production-keystore>
> keytool -list -v -alias releasekey -keystore C:\MyCodeRepo\fluttergithubprojects\xinthink_flt_keep\releaseKey.jks
```


Firebase console'da proje dosyası açılır, Ayarlarda SHA-1 girilir ve kaydedilir.
Güncül google-services.json dosyası indirilir, flutter project içinde Andoid içindeki app klaörüne yüklenir.
c:\path-to\your-flutter-project-folder\android\app\


You are probably missing npm in your path. You can check it by echo %PATH% to make sure. Thus, open Environmental variables > system variables > path
see if you could not find C:\Users\yourusername\AppData\Roaming\npm there. 


firebase login
Firebase CLI ile firebase sistemine bağlantı sağlamış oluruz.

firebase init
Flutter projesinin ana klasöründe iken bu komut ile projemize firebase CLI entegre edilmiş olur.
Seçerken use existing project seçip, sadece functionları seçtik ve typescript seçtik.
Ana klasörümüze firebase.json ve .firebaserc oluşmuş olur.
At the end of initialization, Firebase automatically creates the following two files at the root of your local app directory:
A firebase.json configuration file that lists your project configuration.
A .firebaserc file that stores your project aliases.


firebase deploy --only functions
functions klasörü içindeki src'de varsa index.ts'yi js'e çevirip functions içine koyar ve firebase functions'a deploy eder.

firebase projects:list

# Deploy new function called webhookNew
$ firebase deploy --only functions:webhookNew

# Wait until deployment is done; now both webhookNew and webhook are running

# Delete webhook
$ firebase functions:delete webhook

My personal taste: InheritedWidget/Provider + ValueNotifier/ChangeNotifier + sealedclass (freezed) + BLoC (although this violates BLoC rules). This is a solid approach I don't have any obstacles with this approach so far.