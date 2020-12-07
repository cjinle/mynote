# Linux Bash严重漏洞修复

Linux官方内置Bash中新发现一个非常严重安全漏洞（漏洞参考https://access.redhat.com/security/cve/CVE-2014-6271  ），黑客可以利用该Bash漏洞完全控制目标系统并发起攻击。

### 影响版本
所有安装GNU bash 版本小于或者等于4.3的Linux操作系统。  

### 漏洞描述
该漏洞源于你调用的bash shell之前创建的特殊的环境变量，这些变量可以包含代码，同时会被bash执行。 

### 漏洞检测方法
```
[root@qd1 ~]# env x='() { :;}; echo vulnerable' bash -c "echo this is a test" 
```

修复前输出：
```
vulnerable
this is a test
```

修复后输出：
```
bash: warning: x: ignoring function definition attempt
bash: error importing function definition for `x'
this is a test
```


### 修复方案
```
[root@qd1 ~]# yum -y update bash 
```