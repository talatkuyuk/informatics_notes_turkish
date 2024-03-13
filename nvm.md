https://fedingo.com/how-to-install-nvm-on-mac-with-brew/

nvm install node
nvm install 16
nvm install lts/gallium // alias to LTS v.16.14.2
nvm ls
nvm use 12
nvm use 16
nvm install-latest-npm

uninstall node via nvm
option-1
nvm uninstall <version>
nvm uninstall v16.14.2
option-2
cd ~/.nvm/versions/node
sudo rm -rf v16.14.2
