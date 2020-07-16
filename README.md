# MongoDB-Summary
### Install MongoDB Community Edition on Ubuntu18.04
1. Import the public key used by the package management system.  
`wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -`  
2. Create a list file for MongoDB.  
`echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list`  
3. Reload local package database.  
`sudo apt-get update`  
4. Install the MongoDB packages.  
`sudo apt-get install -y mongodb-org`  
5. Start MongoDB.  
`sudo systemctl start mongod`  
6. Verify that MongoDB has started successfully.  
`sudo systemctl status mongod`  

### Begin using MongoDB.  
`mongo`  
<br />
Create root user:  
```
use admin
db.createUser(
   {user:'root',
    pwd:'123456',
    roles:[{role:'root',db:'admin'}]
   }
)
```
Login:  
```
use admin
db.auth('root', '123456')
```
Use root user to create another user
```
use testdb    
db.createUser({user:'test', pwd:'123456', roles:[{role:'dbOwner', db:'testdb}]})  
use testdb  
db.auth('test','123456')  
```
Add new documents to a collection  
```
db.users.insertOne({name:"turing", age:18, email:'www.163.com'})  
db.users.insertOne({name:'duo', age:20})  
```  
Read collection or documents  
```
show collections  
db.users.find({})  
```
Update existing document in a collection  
```
db.users.updateOne({name:'duo'}, {$set:{email:'www.duoduo.com'}})
```  
Remove document from a collection  
`db.users.deleteOne({name:'turing'})`  
Backup
```
mongodump -h localhost -u root -p root -o /path/to/save  
```  
Restore  
```
mongorestore -h localhost -u root -p 123456 --dir /path/of/data
```  




