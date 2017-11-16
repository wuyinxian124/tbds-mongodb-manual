### 安装mongodb
&emsp;&emsp;mongodb 可以分成三个部分，分别是config server,shard server,router server ,在tbds中也对应三个部分，config和shard 必须安装的部分，router 可以选装。  

**写在最前面**  
config server 和 shard server 是通过mongod 启动的进程。  
router server 是通过mongos 启动的进程。  
config sever 和shard server 可以有对应的arbiter节点(通常会在shard server添加arbiter),如果一个节点被设置为arbiter节点，那么就不能安装其他分片或者备份。

### 安装配置
#### 1. config server
**1.1 config-server-env**  
该文件填写 config server 启动参数，格式必须符合yarml 格式  
默认是使用keyfile 认证模式（keyfile 指定的keyfile 路径不能变化）：  
```
security:
    keyFile: /usr/local/mongodb/cfg/keyfile
```  
**1.2 config-server**   
config_server_db_path 指定config 数据存储路径(完整路径为 /usr/local/mongodb+ 指定路径)    

config_server_log_path 指定log 存储路径(完整路径为 /usr/local/mongodb+ 指定路径)    

mongodb.config.deploy.plan 指定 config 分片和备份规划  
格式为:
```
config1/hostname1:port1,hostname2:port2|config2/hostname3:port3,hostname4:port4,[hostname5:port5]
```
config1 和config2是两个分片名称，config1下面有一主一备，分别是hostname1,hostname2,主备之间是mongodb 内部决定的。通过[] 标示的hostname5 表示该节点是仲裁点，也就是说config2 有一主一备一仲裁。port mongod进程通信端口，请确保指定的端口没有被其他进程占用。

**ps:**  
&emsp;&emsp;需要特别注意的是 仲裁节点不能安装其他分片或者备份  

#### 2. shard server
**2.1 shard-server-env**  
该文件填写 shard server 启动参数，格式必须符合yarml 格式  
默认是使用keyfile 认证模式（keyfile 指定的keyfile 路径不能变化）

**2.2 shard-server-env**  
shard_server_log_path shard 日志存储路径(完整路径为 /usr/local/mongodb+ 指定路径)    

shard_server_db_path 数据存储路径(完整路径为 /usr/local/mongodb+ 指定路径)  

mongodb.shard.deploy.plan shard 分片和备份规划（副本集配置）  
格式为:
```
shard1/hostname1:port1,hostname2:port2|shard2/hostname3:port3,hostname4:port4,[hostname5:port5]
```
shard1 和shard2是两个分片名称,表示整个db会切成两个分片。shard1下面有一主一备，分别是hostname1,hostname2,主备之间是mongodb 内部决定的。通过[] 标示的hostname5 表示该节点是仲裁点，也就是说shard2 有一主一备一仲裁。port mongod进程通信端口，请确保指定的端口没有被其他进程占用。

**ps:**  
&emsp;&emsp;需要特别注意的是 仲裁节点不能安装其他分片或者备份 

#### 3. router server
**3.1 router-server-env**  
该文件填写 router server 启动参数，格式必须符合yarml 格式  
默认是使用keyfile 认证模式（keyfile 指定的keyfile 路径不能变化）：  
```
security:
    keyFile: /usr/local/mongodb/cfg/keyfile
```  
**3.2 router-server**   
router_server_log_path 指定log 存储路径(完整路径为 /usr/local/mongodb+ 指定路径)  

#### 说明
1. 安装过程中，tbds会在mongodb 中新建一个用户admin ,密码是123qwe!@#QWE 目前这个密码是固定的，不能指定。 admin 对应的角色为root,userAdminAnyDatabase。默认启用key file 认证，一旦认证开启，那么后续操作都需要是用到 admin 用户  
2. 首次安装过程会出现告警，这是因为安装的时间差造成的。如果你仔细查看告警，会发现同一个分片中，只有一个节点的成功的，其他节点是失败的，而且router 会直接不启动。出现这个问题的最佳方式是 待首次启动之后，再启动router就行。
3. 如果有修改分片或者副本集，需要重启整个mongodb。
