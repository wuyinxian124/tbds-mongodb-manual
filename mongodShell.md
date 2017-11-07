config和shard 需要通过mongod 命令启动。

1. 启动mongod 进程  
1.1 启动 config server 
启动方式有两种：命令行和配置文件  
命令行：  
```
mongod --configsvr --replSet <setname> --dbpath <path> --port <port> --logpath <logpath> --fork  
```
配置文件：  
```
mongod --config <path-to-config-file>
```
使用配置文件（符合yaml 格式）的方式启动，配置文件的内容通常包括  
```
sharding:
    clusterRole: configsvr
systemLog:
    destination: file
    path: "/usr/local/mongodb/log/cfgserver/mongod.log"
    logAppend: true
processManagement:
    fork: true
net:
    port: 5678
storage:
    dbPath: /usr/local/mongodb/data/cfgdb
    journal:
        enabled: true
replication:
    replSetName: config1
```
如果需要使用keyfile 认证启动需要在配置文件中添加 
```
security:
    keyFile: /usr/local/mongodb/cfg/keyfile
```  
1.2 启动shard server  
启动方式有两种：命令行和配置文件    
命令行： 
``` 
mongod --shardsvr --replSet <setname> --dbpath <path> --port <port> --logpath <logpath> --fork  
```
配置文件：
```
mongod --config <path-to-config-file>
```
使用配置文件（符合yaml 格式）的方式启动，配置文件的内容通常包括
```
sharding:
    clusterRole: shardsvr
systemLog:
    destination: file
    path: "/usr/local/mongodb/log/shardserver/mongod.log"
    logAppend: true
processManagement:
    fork: true
net:
    port: 7896
storage:
    dbPath: /usr/local/mongodb/data/sharddb
    journal:
        enabled: true
replication:
    replSetName: shard1
```
如果需要使用keyfile 认证需要在配置文件中添加：
```
security:
    keyFile: /usr/local/mongodb/cfg/keyfile
```
2. 更多mongod 操作参考：
https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod
