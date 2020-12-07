# 10个最酷的Linux命令

`sudo !!`
以 root 帐户执行上一条命令。

`python -m SimpleHTTPServer`
利用 Python 搭建一个简单的 Web 服务器，可通过 http://$HOSTNAME:8000 访问。

`:w !sudo tee %`
在 Vim 中无需权限保存编辑的文件。

`cd -`
更改到上一次访问的目录。

`^foo^bar`
将上一条命令中的 foo 替换为 bar，并执行。

`cp filename{,.bak}`
快速备份或复制文件。

`mtr google.com`
traceroute + ping。

`!whatever:p`
搜索命令历史，但不执行。

`$ssh-copy-id user@host`
将 ssh keys 复制到 user@host 以启用无密码 SSH 登录。

`ffmpeg -f x11grab -s wxga -r 25 -i :0.0 -sameq /tmp/out.mpg`
把 Linux 桌面录制为视频。