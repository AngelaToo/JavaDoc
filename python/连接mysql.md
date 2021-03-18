python连接mysql数据库

1. 先下载pymysqll模块，进入命令提示符界面运行以下命令

![img](https://img2020.cnblogs.com/blog/2184653/202012/2184653-20201212152306650-131315702.png)

 在python中执行以下命令可查询数据库

```
import pymysql#调用模块
db = pymysql.connect(user ='root',password='wbf980728',database='wang',charset='utf8')
# 打开数据库连接
cursor = db.cursor()#获取操作游标
demo = cursor.execute('select * from students')#运行SOL语句
lists = cursor.fetchall()#接收返回的结果
print(lists)
for i in lists:
	print(i)
```

在python中操作mysql数据库增删改数据

```
import pymysql#调用模块
db = pymysql.connect(user = 'root',password='wbf980728',database='wang',charset='utf8')
#打开数据库连接
cursor = db.cursor()#获取操作游标
demo = cursor.execute('INSERT INTO students (s_id,c_id,s_name,s_gender,s_score) VALUES (9,4, "零零", "女", 77)')
demo = cursor.execute('DELETE  FROM students WHERE s_id=8')
demo = cursor.execute('UPDATE students SET s_name="kk", s_score=66 WHERE s_id=1;')
lists = cursor.fetchall()#接收返回的值
db.commit()#提交mysql语句
print(demo)
```

关闭数据库

```
import pymysql#调用模块
db = pymysql.connect(user = 'root',password='wbf980728',database='wang',charset='utf8')
#打开数据库连接
cursor = db.cursor()#获取操作游标
data=db.close() #关闭数据库
print(data)
```