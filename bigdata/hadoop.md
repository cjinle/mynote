# hadoop

## 入门

_历史 lucene --> natch --> hadoop_


### google大数据三篇论文
 - GFS --> HDFS
 - Map-Reduce --> MR
 - BigTable --> HBase

### 三大发行版本
 - apache
 - cloudera
 - hortonworks

## Common辅助工具

## MapReduce计算
 - Map阶段并行处理输入数据
 - Reduce阶段对Map结果进行汇总

## HDFS存储
 - NameNode(nn) 存储文件的元数据
 - DataNode(dn) 本地文件系统存储块数据
 - Secondary NameNode(2nn) 监控HDFS状态的辅助后台程序

## Yarn资源调度
 - ResourceManager(RM) 
    - 处理客户端请求
    - 监控NodeManager
    - 启动监控ApplicationMaster
    - 资源的分配与调度
 - NodeManager(NM)
    - 管理单个节点上的资源
    - 处理来自ResourceManager的命令
    - 处理来自ApplicationMaster的命令

## 技术生态体系

0x01  第15课时 



