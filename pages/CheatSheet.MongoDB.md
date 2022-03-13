- **准备工作**
	- Initiate
		- ```python
		  import pymongo
		  import urllib
		  from pymongo import MongoClient
		  password = urllib.parse.quote('your-pass-word')
		  username = urllib.parse.quote('your-user-name')
		  uri = f'mongodb+srv://{username}:{password}@.....'
		  myclient = MongoClient(uri)
		  ```
	- Check if database exists
		- ```python
		  print(myclient.list_database_names())
		  ```
	- Check if collection exists
		- ```python
		  print(mydb.list_collection_names())
		  ```
- **Creating a Collection**
	- ```python
	  myclient = pymongo.MongoClient("mongodb://localhost:27017/")
	  mydb = myclient["mydatabase"]
	  mycol = mydb["customers"]
	  ```
- **Insert into Collection**
	- Insert one
		- ```python
		  mydict = {"name": "John", "address": "Highway 37"}
		  x = mycol.insert_one(mydict)
		  
		  # return the _id field
		  print(x.inserted_id)
		  ```
	- Insert multiple document
		- ```python
		  import pymongo
		  myclient = pymongo.MongoClient("mongodb://localhost:27017/")
		  mydb = myclient["mydatabase"]
		  mycol = mydb["customers"]
		  # _id 必须是唯一值, 如果不指定, 系统自动生成_id
		  mylist = [
		    { "_id": 1, "name": "John", "address": "Highway 37"},
		    { "_id": 2, "name": "Peter", "address": "Lowstreet 27"},
		    { "_id": 3, "name": "Amy", "address": "Apple st 652"},
		  ]
		  x = mycol.insert_many(mylist)
		  #print list of the _id values of the inserted documents:
		  print(x.inserted_ids)
		  ```
- ^^Find (选取数据)^^
	- Find One 从collection选取^^第一个^^document
		- ```python
		  myclient = pymongo.MongoClient("mongodb://localhost:27017/")
		  mydb = myclient["mydatabase"]
		  mycol = mydb["customers"]
		  x = mycol.find_one()
		  print(x)
		  ```
	- Find All ^^选取全部^^
		- ```python
		  for x in mycol.find():
		    print(x)
		  ```
	- Find with ^^limit^^
		- ```python
		  myresult = mycol.find().limit(5)
		  #print the result:
		  for x in myresult:
		    print(x)
		  ```
	- Return only some fields ^^选取一部分^^
		- ```python
		  for x in mycol.find({},{ "_id": 0, "name": 1, "address": 1 }):
		    print(x)
		  # 其中, 0 表示不要这一列, 1 表示要这一列
		    
		  # 或者以下用法, 找到address为Park Lane 38的记录
		  myquery = { "address": "Park Lane 38" }
		  mydoc = mycol.find(myquery)
		  for x in mydoc:
		    print(x)
		  ```
- **Find with** [[regular expression]]
	- ```python
	  myquery = { "address": { "$regex": "^S" } }
	  mydoc = mycol.find(myquery)
	  for x in mydoc:
	    print(x)
	  ```
- **Sort Result**
	- ```python
	  mydoc = mycol.find().sort("name")
	  for x in mydoc:
	    print(x)
	  
	  # 升序降序
	  sort("name", 1) #ascending
	  sort("name", -1) #descending
	  ```
- **Delete Document**
	- 删除一个
		- The first parameter of the `delete_one()` method is a query object defining which document to delete.
		- ```python
		  myquery = { "address": "Mountain 21" }
		  mycol.delete_one(myquery)
		  ```
	- 删除多个
		- ```python
		  myquery = { "address": {"$regex": "^S"} }
		  x = mycol.delete_many(myquery)
		  print(x.deleted_count, " documents deleted.")
		  ```
	- 全部删除
		- ```python
		  x = mycol.delete_many({})
		  print(x.deleted_count, " documents deleted.")
		  ```
- **Delect Collections**
	- ```python
	  mydb = myclient["mydatabase"]
	  mycol = mydb["customers"]
	  mycol.drop()
	  ```
- **Update Collection**
	- update_one
		- ```python
		  mydb = myclient["mydatabase"]
		  mycol = mydb["customers"]
		  
		  # Change the address from "Valley 345" to "Canyon 123" 其中$set为操作符
		  myquery = { "address": "Valley 345" }
		  newvalues = { "$set": { "address": "Canyon 123" } }
		  mycol.update_one(myquery, newvalues)
		  #print "customers" after the update:
		  for x in mycol.find():
		    print(x)
		  ```
	- update_many
		- ```python
		  myquery = { "address": { "$regex": "^S" } }
		  newvalues = { "$set": { "name": "Minnie" } }
		  x = mycol.update_many(myquery, newvalues)
		  print(x.modified_count, "documents updated.")
		  ```
- **条件操作符**
	- 大于小于
		- ```python
		  # (>) 大于 - $gt
		  # (<) 小于 - $lt
		  # (>=) 大于等于 - $gte
		  # (<= ) 小于等于 - $lte
		  x = prizes_collection.find(
		      {'year': {'$gt':'2020'}}
		  )
		  for i in x:
		    print(i)
		  
		  .find({"age" : {"$gte" : 18, "$lte" : 30}})
		  ```
	- OR 查询
		- ```python
		  # $in
		  db.raffle.find({"ticket_no" : {"$in" : [725, 542, 390]}})
		  # $nin
		  db.users.find({"user_id" : {"$in" : [12345, "joe"]})
		  # $or
		  db.raffle.find({"$or" : [{"ticket_no" : 725}, {"winner" : true}]})
		  db.raffle.find({"$or" : [{"ticket_no" : 
		                            {"$in" : [725, 542, 390]}},
		                           {"winner" :true}]})
		  
		  ```
- 索引
	- 有索引就直接可以在索引查找, 更快, 不用索引的查询被称为全表索引