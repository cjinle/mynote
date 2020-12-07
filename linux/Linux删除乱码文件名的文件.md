# Linux删除乱码文件名的文件

如果服务器上有一些已经是乱码文件名的文件，你又想删除它，这个时候可以通过文件的inode进行删除

```
root@sz2:~# ls -i
1452178 ???????      1452196 bak_web.sh  1452161 composer-setup.php  1452175 lok.php
1452095 20170630.7z  1452155 bb.php      1452157 dedecms.log         1452159 ss.pouman.com
1452160 aa.php       1452192 bypy.log    1452162 ds.sh               1452181 start_ngrok.sh
1452195 bak_db.sh    1452165 code        1452158 kill_php.sh         1452164 vpn_start.sh
root@sz2:~# find -inum 1452178
./???????
root@sz2:~# find -inum 1452178 -delete
root@sz2:~# ls
20170630.7z  bak_db.sh   bb.php    code                dedecms.log  kill_php.sh  ss.pouman.com   vpn_start.sh
aa.php       bak_web.sh  bypy.log  composer-setup.php  ds.sh        lok.php      start_ngrok.sh
```