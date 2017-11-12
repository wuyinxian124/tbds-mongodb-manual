router 进程启动是通过mongos 命令操作

1. 启动mongos 进程  
router server 启动方式有两种：命令行和配置文件    
1.1 命令行方式  
启动命令：
```
  mongos --configdb <configReplSetName>/cfg1.example.net:27019,cfg2.example.net:27019 --port 20000 --logpath <logpath> --fork
```
1.2 配置文件  
启动命令：
```
mongos --config <path-to-config>
```
使用配置文件(配置文件符合yaml 格式)的方式启动，配置文件通常添加如下内容：
```
systemLog:
    destination: file
    path: "/usr/local/mongodb/log/routerserver/mongod.log"
    logAppend: true
processManagement:
    fork: true
net:
    port: 20000
sharding:
    configDB: config1/tbds-10-151-136-16:5678,tbds-10-254-96-17:5678
```
如果需要使用认证，需要在配置文件中添加如下内容：
```
security:
    keyFile: /usr/local/mongodb/cfg/keyfile
```
