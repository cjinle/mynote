# Windows下的crontab设置

需求：因为公司电脑网络问题，导致虚拟机的网络有问题
必须要重启虚拟机才能解决，所以就想着设置一个定时的执行的重启脚本


### 定时设置

```bat
# 任务查询
schtasks /query
# 创建任务
schtasks /create /tn "xp_vm_reset" /tr "D:\xp_vm_reset.bat" /sc hourly /mo 1
# 执行任务
schtasks /run /tn "xp_vm_reset"
# 删除任务
schtasks /delete  /tn "xp_vm_reset"
# 停止任务
schtasks /end /tn "xp_vm_reset"
```

详细的配置详情可以参考微软的[官方文档](https://technet.microsoft.com/en-us/library/cc721871(v=ws.11).aspx)


### 重启虚拟机的脚本(xp_vm_reset.bat)
```bat
"C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" controlvm xp reset
```

其实原理还是很简单的。