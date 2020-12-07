# Vim不保留备份文件

Vim默认是保留备份文件的，如 `aa.py~` 的~结尾的文件，

虽然很有用，但实在和自己使用很不习惯。

下面是不保留备份文件配置，

## Windows:
下面是Windows下Vim的默认安装路径，
修改此文件， `C:\Program Files\Vim\_vimrc`
新增一行
`set nobackup`

重启Vim就OK

## Linux:
`~/.vimrc`
同样加上`set nobackup`


