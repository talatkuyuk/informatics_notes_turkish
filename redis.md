## Redis

### Install Redis on Mac With Homebrew
brew install redis

### Start Redis Server
brew services start redis

### Test if Redis Server is Running  
redis-cli ping  
*The system responds with a ‘pong’ if the server is up and running.*

### Uninstalling Redis on Mac
brew uninstall redis


### see Redis version
redis-cli --version


brew services start redis
brew services stop redis
brew services restart redis