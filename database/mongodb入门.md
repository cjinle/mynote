# mongodb 入门

## 安装
__环境__: debian9

```sh
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
sudo apt-get install gnupg
echo "deb http://repo.mongodb.org/apt/debian stretch/mongodb-org/4.4 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod

# optional
sudo systemctl daemon-reload
sudo systemctl status mongod
sudo systemctl enable mongod
sudo systemctl stop mongod
sudo systemctl restart mongod
mongo # client
```

### 测试
```js
show dbs;
use test;
db.testcol.insert({name:"chenjinle"});
db.testcol.find();
```

## 增删改查

### 查询数据
```js
db.testcol.find()
db.testcol.findOne()

db.testcol.find({"size.uom": "in"}) // 内嵌条件
db.testcol.find({"size.h", {$lt: 15}})
```

### 增加数据
```js
db.testcol.insert({name:"chenjinle"})
db.testcol.insertOne({name:"chenjinle"})
db.testcol.insertMany([{name:"zhangsan"},{name:"lisi"}])
```

### 修改数据
```js
db.testcol.update({"name":"chenjinle"},{name:"cjinle"})

db.testcol.updateOne()
db.testcol.updateMany()
db.testcol.replaceOne()
```

### 删除数据
```jsp
db.testcol.remove({"name":"zhangsan"})

db.testcol.deleteOne()
db.testcol.deleteMany()
```

## 备份恢复

### 备份
```sh
mongodump
```

### 恢复
```sh
mongorestore -h 127.0.0.1:27017 -d test ~/dump/test/
```

