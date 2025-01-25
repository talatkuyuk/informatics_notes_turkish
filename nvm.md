https://fedingo.com/how-to-install-nvm-on-mac-with-brew/

nvm install node
nvm install 16
nvm install lts/gallium // alias to LTS v.16.14.2
nvm ls
nvm use 12
nvm use 16
nvm install-latest-npm

## to see node versions installed via nvm

https://nodejs.org/en/about/previous-releases

nvm list

node -> stable (-> v22.12.0) (default)
stable -> 22.12 (-> v22.12.0) (default)
lts/\* -> lts/jod (-> v22.12.0)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0 (-> N/A)
lts/dubnium -> v10.24.1 (-> N/A)
lts/erbium -> v12.22.12 (-> N/A)
lts/fermium -> v14.21.3 (-> N/A)
lts/gallium -> v16.20.2 (-> N/A)
lts/hydrogen -> v18.20.5
lts/iron -> v20.18.1
lts/jod -> v22.12.0

## to update node versions

nvm list
nvm use 20
nvm current
nvm install lts/iron --reinstall-packages-from="$(nvm current)"
nvm uninstall v20.0.0

## to uninstall node via nvm

option-1
nvm uninstall <version>
nvm uninstall v16.14.2
option-2
cd ~/.nvm/versions/node
sudo rm -rf v16.14.2
