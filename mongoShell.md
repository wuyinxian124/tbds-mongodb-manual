写在最前面:  
&emsp;&emsp;mongo shell 是mongodb 提供的一种基于javascript命令行交互方式。通过该命令可以操作和管理mongodb 数据库。  

1. 连接
```
bin/mongo --host <hostname> --port <port>
```

mongo shell种类很多 包括：  
Collection  
Cursor  
Database  
Query Plan Cache  
Bulk Write Operation  
User Management  
Role Management  
Replication  
Sharding  
Subprocess  
Constructors  
Connection  
Native  
更多参考：  
https://docs.mongodb.com/manual/reference/method/  

但是常用的有[Database](databaseMethods.md),[Replication](replicationMethods.md),[Sharding](shardingMethods.md),[User Management](userManagerMethods.md) 。其他的以后讨论。
