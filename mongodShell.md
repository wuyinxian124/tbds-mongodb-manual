config和shard 需要通过mongod 命令启动。

1. 启动mongod 进程  
启动方式有两种：命令行和配置文件  
命令行：  
/usr/local/mongodb//bin/mongod --configsvr --replSet cfgReplSet6 --dbpath /usr/local/mongodb/data/cfgdb --port 53000 --logpath /usr/local/mongodb/log/cfgserver/cfgserver0.log --fork
配置文件：  


2. 
