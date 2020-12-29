
npm install -g firebase-tools

if error happens for access
https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

firebase --version

firebase login

mkdir firebase-functions
cd firebase-functions

firebase init

functions > existing project > select a project > eslint NO > JavaScript > intal dependencies YES

cd functions

index.js'te HelloWorld function uncomment et.
```javascript
// Create and Deploy Your First Cloud Functions
// https://firebase.google.com/docs/functions/write-firebase-functions
//
exports.helloWorld = functions.https.onRequest((request, response) => {
  functions.logger.info("Hello logs!", {structuredData: true});
  response.send("Hello from Firebase!");
});
```

firebase deploy

Örnek Sonuç:
Function URL (helloWorld): https://us-central1-socialapp-cc8a8.cloudfunctions.net/helloWorld

Function Call with Postman
Postman'de > https://us-central1-socialapp-cc8a8.cloudfunctions.net/helloWorld

index.js dosyasında getScreams function yaratalım.

firebase deploy

Postman'de > https://us-central1-socialapp-cc8a8.cloudfunctions.net/getScreams

function kod örnekleri için bak
https://firebase.google.com/docs/firestore/query-data/get-data

function'ları deploy etmek zaman alıyor, function call api'lerinin localhostta çalışması için localde firebase emulatörü kurabiliriz.
> firebase serve  (artık önerilmiyor)
> firebase emulators:start 

package.json dosyasındaki scriptler npm run <komut> şeklinde kullanılabilir. 
> npm run deploy
> npm run serve

firebase init komutu ile functions ve admin paketi kurulmuştu. Diğer firebase paketlerini (storage, authentication, firestore vb.) kullanmak için:
> npm i --save firebase

functions klasörü içerisinde bir nodejs uygulaması geliştirebiliriz. Aşağıdaki paketler faydalı.
> npm i --save express cors uuidv4

