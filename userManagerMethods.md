参考：  
https://docs.mongodb.com/manual/reference/command/nav-user-management/  

常用

1. db.createUser()  
创建用户
```
db.createUser(
  {
    user: "testadmin",
    pwd: "admin@123",
    roles: [ { role: "root", db: "admin" } ]
  }
);
```

2. db.getUsers()   
查询用户信息  
3. db.getUser("admin")  
查询admin用户是否存在  
