- #### 远程连接

   mongo ip:port/dbname -u 用户名 -p 密码

- #### 创建数据库

   `use DATABASE_NAME` 

- #### 查看所有数据库|查看当前数据库

    `show dbs` `| db`

- 查看所有集合

    ```dart
    show tables | show collections
    ```

    #### mongo中的操作符

    ```bash
    # 以 $ 开头
    $set # 更新字段
    $unset # 删除字段
    $inc  # 自增  {$inc: {money: 10}} | 自减 {$inc: {money: -10}}
    $exists # 是否存在
    $in # 是否在...范围
    $and
    $or
    $push  # 向数组中尾部添加一个元素
    $addToSet # 向集合中添加元素
    $pop  # 删除数组中的头部或尾部元素
    ```

    ####  mongo运算符 

    ```bash
    $eq 等于
    $ne 不等于
    $gt 大于
    $gte 大于等于
    $lt 小于
    $lte 小于等于
    $in 在范围内
    $nin 不在范围内
    ```

- #### 向数据库插入文档（json格式）

  ` db.COLLECTION_NAME.insert(document)  `

  ```
  >db.col.insert({title: 'MongoDB 教程',
  	description: 'MongoDB 是一个 Nosql 数据库',
  	by: 'MongoDB中文网', 
  	url: 'http://www.mongodb.org.cn', 
  	tags: ['mongodb', 'database', 'NoSQL'],
  	likes: 100  
  })
  
  db.km_test.insert({"name":"xianan","area":"wuhan","status":"working"})
  ```

- #### 查看已插入文档

`db.COLLECTION_NAME.find()`

- #### 删除文档

```json
db.collection.remove( 
​	<query>,     
​	<justOne> 
) 

// mongodb 2.6版本
/* 参数说明：
query :（可选）删除的文档的条件。
justOne : （可选）如果设为 true 或 1，则只删除一个文档。
writeConcern :（可选）抛出异常的级别。*/

db.collection.remove(     
	<query>,     
	{       
		justOne: <boolean>,
		writeConcern: <document> 
	} 
)

db.km_test.remove({"name":"kemian"})
```

- #### 更新文档

  ##### update() 方法 , 用于更新已存在的文档 

1. ```json
   1. db.collection.update(    
   2. ​	<query>, 
   3. ​	<update>, 
   4. ​	{       
   5. ​		upsert: <boolean>,   
   6. ​		multi: <boolean>,  
   7. ​		writeConcern: <document>
   8. ​	}
   9. )
   
   参数说明：
   query : update的查询条件，类似sql update查询内where后面的。
   update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
   upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
   multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
   writeConcern :可选，抛出异常的级别。
   
   db.km_test.update({"name":"kemian"},{$set:{"area":"huangshi"}})
   ```

   ##### save() 方法, 通过传入的文档来替换已有文档 

```json
db.collection.save(    
	<document>,     
	{      
		writeConcern: <document> 
	}  
)  
参数说明：

document : 文档数据。
writeConcern :可选，抛出异常的级别

db.km_test.save({
    "_id" : ObjectId("5ed06f4eb9f72c1241ae1a64"),
    "name" : "kemian",
    "area" : "huangshi",
    "status" : "busy"
})

//查看
db.km_test.find().pretty()
```

####  游标操作之skip 

```css
相当于mysql的 limit 3,5
限制查询的起始位置,和返回指定的数量的数据
db.users.find().skip(3).limit(5);
```

- #### 索引

##### 查询限制

索引不能被以下的查询使用：

- 正则表达式及非操作符，如 $nin, $not, 等。
- 算术运算符，如 $mod, 等。
- $where 子句

所以，检测你的语句是否使用索引是一个好的习惯，可以用explain来查看。

```json
db.km_test.find().pretty().explain()
```



#### 最大范围

- 集合中索引不能超过64个
- 索引名的长度不能超过125个字符
- 一个复合索引最多可以有31个字段

## ensureIndex() 方法 创建索引 

```
  \>db.COLLECTION_NAME.ensureIndex({KEY:1})   
```

 语法中 Key 值为你要创建的索引字段，1为指定按升序创建索引，如果你想按降序来创建索引指定为-1即可。 

```
db.km_test.ensureIndex({"name":1})
```

## MapReduce 命令

 被用来构建大型复杂的聚合查询 

```
>db.collection.mapReduce(
   function() {emit(key,value);},  //map 函数
   function(key,values) {return reduceFunction},   //reduce 函数
   {
      out: collection,
      query: document,
      sort: document,
      limit: number
   }
)

使用 MapReduce 要实现两个函数 Map 函数和 Reduce 函数,Map 函数调用 emit(key, value), 遍历 collection 中所有的记录, 将key 与 value 传递给 Reduce 函数进行处理。

Map 函数必须调用 emit(key, value) 返回键值对。

参数说明:

map ：映射函数 (生成键值对序列,作为 reduce 函数参数)。
reduce 统计函数，reduce函数的任务就是将key-values变成key-value，也就是把values数组变成一个单一的值value。。
out 统计结果存放集合 (不指定则使用临时集合,在客户端断开后自动删除)。
query 一个筛选条件，只有满足条件的文档才会调用map函数。（query。limit，sort可以随意组合）
sort 和limit结合的sort排序参数（也是在发往map函数前给文档排序），可以优化分组机制
limit 发往map函数的文档数量的上限（要是没有limit，单独使用sort的用处不大）

```

#### Mongodb聚合

## aggregate() 方法

MongoDB中聚合的方法使用aggregate()。

```json
>db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)  
```

| 表达式    | 描述                                           | 实例                                                         |
| :-------- | :--------------------------------------------- | :----------------------------------------------------------- |
| $sum      | 计算总和。                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}]) |
| $avg      | 计算平均值                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}]) |
| $min      | 获取集合中所有文档对应值得最小值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}]) |
| $max      | 获取集合中所有文档对应值得最大值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}]) |
| $push     | 在结果文档中插入值到一个数组中。               | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}]) |
| $addToSet | 在结果文档中插入值到一个数组中，但不创建副本。 | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}]) |
| $first    | 根据资源文档的排序获取第一个文档数据。         | db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}]) |
| $last     | 根据资源文档的排序获取最后一个文档数据         | db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}]) |



1.数据存到内存中，查询速度快

2.存储方便，json格式存入和取出，方便使用

2.实体容易增加|减少字段，持久化的话这块要查下

#### example:

```json
db.getCollection("orders_443").find({"mobile":"12345678900","state": {$ne:"10"}}).sort({"create_date":-1}).limit(1)
```

