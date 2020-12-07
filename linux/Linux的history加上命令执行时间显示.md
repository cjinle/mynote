# Linux的history加上命令执行时间显示

默认`history`命令，仅仅显示历史命令列表，如何显示该命令执行的时间呢？

其实比较简单，要全局有效的话，就修改`/etc/bashrc`，如果是当前用户，则修改`$HOME/.bash_profile`

只要加上

```
export HISTTIMEFORMAT="[%Y-%m-%d %H:%I:%S] "
```

**更新变量文件**
```
[root@server1 ~]# source /etc/bashrc
[root@server1 ~]# source $HOME/.bash_profile
```

**效果**
```
   21  [2012-05-10 19:07:22] ls
   22  [2012-05-10 19:07:29] source $HOME/.bash_profile 
   23  [2012-05-10 19:07:31] ls
   24  [2012-05-10 19:07:34] ls
   25  [2012-05-10 19:07:35] cd /
   26  [2012-05-10 19:07:35] ls
   27  [2012-05-10 19:07:43] cd
   28  [2012-05-10 19:07:44] ls
   29  [2012-05-10 19:07:49] vim .bash_profile 
```