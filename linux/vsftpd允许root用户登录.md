# vsftpd允许root用户登录

Linux下安装vsftpd之后，默认的配置是
匿名用户可以登录，匿名帐户有两个：
用户名：anonymous
密码：空

用户名：ftp
密码：ftp

如果要用匿名进行上传删除等操作需要配置其它参数。

本篇文章主要是设置如何让root用户可以登录的。
因为默认配置是不行。 

主要在`vsftpd.conf`的两个参数控制
userlist_enable和pam_service_name
默认userlist_enable是YES的状态，pam_service_name是vsftpd

你需要在`/etc/vsftpd/user_list`文件中把root那一行删除或者注释掉
同理，`/etc/vsftpd/ftpusers`文件中的root也注释掉

然后重启`vsftpd`就可以了

*注：实际应用中，允许root用户登录ftp不是一个好习惯！！！*

这个主要是在测试环境中，允许root用户登录操作，方便点，避免了权限的问题

