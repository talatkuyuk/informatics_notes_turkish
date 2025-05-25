cors paketi için güzel bir anlatım.

https://www.gencayyildiz.com/blog/node-js-cors-paketiyle-access-control-allow-origin-guvenlik-yonetimi/

## node.js ve npm versiyonunu görmek için

```powershell
> node -v
> npm -v
```

## Sıfır bir projede package.json oluşturmak için

```powershell
> npm init
```

## Sıfır bir projede sorulara direkt yes diyerek package.json oluşturmak için

```powershell
> npm init -y
```

## İndirilen bir projede package.json'da belirtilen paketlerin tümünü kurmak için

```powershell
> npm install
```

## İndirilen bir projede package.json'da belirtilen paketlerin tümünü ancak projede listelenen versiyonları aynen kurmak için

```powershell
> npm ci
```

## gerçekte install edilen ve node_modules içine yüklenen paket sürümlerini görmek için (bu sayede package.json'da belirtilen paketlerin sürümlerindeki hatalı versiyonlar görülebilir )

```powershell
> npm ls --depth=0
```

## projedeki bir dependency'nin hangi dependency'e bağlı olduğunu anlamak

```powershell
> npm ls paket_ismi
> npm ls paket_ismi --all
```

## paketlerin yeni versiyonları çıkanlarını görmek için

```powershell
> npm outdated  // wanted ve latest alanları gösteriliyor
```

## Sistemde global olarak kurulu paketleri görmek için

```powershell
npm list -g --depth=0
```

## Projede kurulu paketleri görmek için

```powershell
npm list --depth=0
```

## paketleri güncellemek için

```powershell
> npm update
```

wanted versiyonuna yükseltir, ama öncesinde packege.json dosyasında versiyon numaralarını wanted versiyonları olacak şekilde kendin yaz, öbür türlü json dosyasına kaydetmedi, ama aslında outdated olanlarını update etmişti.

## paket yüklemek için

```powershell
> npm i paket
> npm install --save paket

> npm install --save-dev paket
> npm install --D paket
```

## globale paket yüklemek için

```powershell
> npm install -g paket
> npm i -g paket
```

## paket kaldırmak için

```powershell
> npm uninstall paket
```

## paketi globalden kaldırmak için

```powershell
> npm uninstall -g paket
```

## Bir paketi yüklemeden çalıştırmak için

```powershell
> npx create-react-app firebase-react-auth
```

## Install edilmiş bir paketin yerini dependency ve devDependency arasında yer değiştirmek için

```powershell
npm install <module_name> --save-prod
npm install <module_name> --save-dev
```

i install  
-g global  
-D --save-dev  
-y all yes  
-v version

## npm global paketlerinin yerini öğrenmek için

> npm config get prefix
> burasının bin'inde /bin

## install node on MacOS

https://medium.com/@hayasnc/how-to-install-nodejs-and-npm-on-mac-using-homebrew-b33780287d8f

> brew install node I don't use it any more, I use nvm

> node -v  
> node --version  
> npm -v  
> npm --version

## upgrade node on MacOS I don't use it any more, I use nvm

> brew update  
> brew upgrade node
> brew link --overwrite node

## uninstall node from MacOS

https://stackabuse.com/how-to-uninstall-node-js-from-mac-osx/
https://stackoverflow.com/questions/11177954/how-do-i-completely-uninstall-node-js-and-reinstall-from-beginning-mac-os-x

Run following commands to remove node completely from system in MACOS

sudo rm -rf ~/.npm ~/.nvm ~/node_modules ~/.node-gyp ~/.npmrc ~/.node_repl_history
sudo rm -rf /usr/local/bin/npm /usr/local/bin/node-debug /usr/local/bin/node /usr/local/bin/node-gyp
sudo rm -rf /usr/local/share/man/man1/node* /usr/local/share/man/man1/npm*
sudo rm -rf /usr/local/include/node /usr/local/include/node_modules
sudo rm -rf /usr/local/lib/node /usr/local/lib/node_modules /usr/local/lib/dtrace/node.d
sudo rm -rf /opt/local/include/node /opt/local/bin/node /opt/local/lib/node
sudo rm -rf /usr/local/share/doc/node
sudo rm -rf /usr/local/share/systemtap/tapset/node.stp

> brew uninstall node (if not works since there is a dependency like http-server, try below)
> brew uninstall --ignore-dependencies node
> brew doctor
> brew cleanup --prune-prefix
> ########################################################
