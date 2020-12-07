# linux下systemctl命令简单使用

## 例子

启动一个服务：`systemctl start nginx`
关闭一个服务：`systemctl stop nginx`
重启一个服务：`systemctl restart nginx`
重载一个服务：`systemctl reload nginx`
显示一个服务的状态：`systemctl status nginx`
在开机时启用一个服务：`systemctl enable nginx`
在开机时禁用一个服务：`systemctl disable nginx`
查看服务是否开机启动：`systemctl is-enabled nginx`
查看已启动的服务列表：`systemctl list-unit-files | grep enabled`

查看启动失败的服务列表：`systemctl --failed`