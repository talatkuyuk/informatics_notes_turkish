##### installation
brew tap mongodb/brew
brew install mongodb-community@5.0

#####  The installation includes the following binaries:
**mongod** server
**mongos** sharded cluster query router
**mongosh** the MongoDB shell, 

brew services start mongodb-community@5.0  
brew services stop mongodb-community@5.0


#### Local MongoDB Instance on Default Port
mongosh
mongosh "mongodb://localhost:27017"
mongo --version
