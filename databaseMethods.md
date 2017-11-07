
参考：  
https://docs.mongodb.com/manual/reference/method/js-database/  

-------
常用
1. db.shutdownServer()  
	停止当前mongod或者是mongos 进程。
2. db.stats()	  
  当前db 的状态，包括shard 集合信息
3. db.serverStatus()
  当前db 进程状态，包括config 集合信息
4. db
显示当前db

5. use admin
切换db
