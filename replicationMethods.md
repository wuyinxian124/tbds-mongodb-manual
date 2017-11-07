参考：  
https://docs.mongodb.com/manual/reference/method/#replication  


1. rs.add()  
	集合中添加一个新的节点
2. rs.addArb()	 
  集合中添加一个仲裁节点  
3. rs.initiate()   
	Initializes a new replica set.
4. rs.remove()	
Remove a member from a replica set.  
5. rs.status()    
	返回副本集信息，如果是在shard登陆就是shard 集合信息，如果是config 登陆，返回的就是config 信息。 
