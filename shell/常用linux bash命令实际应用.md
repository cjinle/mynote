# 常用linux bash命令实际应用

常用linux bash命令实际应用，按大小排序。

```bash
ls|xargs du -h|sort -rn 
#不递归下级目录使用du -sh
```

查看文件排除以#开关和空白行，适合查看配置文件。
```bash
egrep -v "^#|^$"  filename
sed '/#.*$/d; /^ *$/d'
```

删除空格和空行。
```bash
sed '/^$/d' filename #删除空行
sed -i '/^\s*$/d' filename #多个空格组成的空行
sed 's/ //g' filename
sed 's/[[:space:]]//g' filename
```

linux换行\n转为windows换行\r\n：
```bash
perl -pi -e 's/\n/\r\n/'  filename
```

windows下多行之前空行，原因是双换行符^M，删除一个：
```bash
#^M输入方法Ctrl v + Ctrl m
 sed -i 's/^M^M/^M/g' filename
#单独一行就一个换行符
sed -i '/^^M/d' filename
```

删除#后的注释。
```bash
sed -i 's/#.*$//g' filename
```

踢出登录的用户，用who查看终端。
```bash
pkill -KILL -t pts/0
```

删除空文件。
```bash
find / -type f -size 0 -exec rm -rf {} \;
```

查找进程pid并kill。
```bash
pgrep nginx|xargs kill
pidof nginx|xargs kill
```

获取当前IP地址，强大的awk，一个命令搞定。
```bash
ifconfig |awk -F"[ ]+|[:]" 'NR==2 {print $4}'
```

文本方式查看wtmp日志
```bash
utmpdump /var/log/wtmp
```

以内存大小排序列出进程
```bash
ps aux --sort=rss |sort -k 6 -rn
```

简单web server列出当前目录文件，端口8000：
```bash
python -m SimpleHTTPServer
```

以管道输入方式修改用户密码：
```bash
echo "password" |passwd –stdin root
```

生成SSH证书并复制到远端服务器：
```bash
ssh-keygen -y -f ~/.ssh/id_rsa &&　cat ~/.ssh/id_rsa.pub | ssh root@host "cat - >> ~/.ssh/authorized_keys"
```

shell下新建文件夹并进入，以下加入bashrc：
```bash
mkcd ( ){
mkdir $1
cd $1
}
```

通过SSH快速备份文件到另一服务器：
```bash
tar zcvf - back/ | ssh root@dev.test.com tar xzf - -C /root/back/
```

用wget下载整站：
```bash
wget -r -p -np -k http://dev.test.com
#r递归 p下载所有文件 np不下载上级 k转换相对链接
```

Kill整个进程树：
```bash
pstree -ap 10277|grep -oP '[0-9]{4,6}'|xargs kill -9
```

生成随机字符：
```bash
cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 32 | head -n 1
```

使用awk导出最后一列非空的数据：
```bash
awk -F "|" '{if($NF!="") print $NF}'
```

查找每行大于几位数的数据：
```bash
awk -F '' '{if(NF>6) print $0}'
```

获取HTML页面文本内容：
```bash
lynx -dump dev.test.com #包含页面的URL
w3m -no-cookie -dump dev.test.com
links -dump dev.test.com #对中文内容支持不好
```

端口重定向：
```bash
socat TCP4-LISTEN:1234,reuseaddr,fork, TCP4:www.baidu.com:80
```

行前或行后插入：
```bash
sed 'p;s/^.*$/--------/' file
awk '{print $0;print "-------"}' file
```

行首或行尾插入：
```bash
sed 's/^/new/g' file
sed 's/$/new/g' file
```

逐字换行：
```bash
awk -F "" '{for(i=1;i<=NF;i++) print $i}'
```

目录中大量文件删除：
```bash
ls | xargs rm
```

文本去重复：
```bash
sort -u file.txt
#或使用uniq，只能去除连续重复的行，先用sort排序再用uniq去重
sort file.txt|uniq
```