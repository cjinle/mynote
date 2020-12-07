# centos6清除iptables,selinux规则

安装完默认centos6后，会有默认的一些iptables,selinux规则，
当然是这系统为了安全考虑，但对于我们一般做测试练习来讲，
是不必要的问题，难以去定位环境问题所在。

### 清除iptables规则
```bash
iptables -F
service iptables save
service iptables restart
```

### 关闭selinux
```bash
setenforce 0
```

编辑配置文件：`/etc/selinux/config`，设置`SELINUX=disabled`
```bash
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of these two values:
#     targeted - Targeted processes are protected,
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```
