# Let’s Encrypt泛域名免费ssl证书

现在免费证书除了上一篇文章阿里的外，还有另一个Let’s Encrypt的免费证书，缺点是有效期只有3个月，
优点就是免费，还支持泛域名。

## 安装申请证书工具
```sh
apt-get update && apt-get install curl -y && apt-get install cron -y && apt-get install socat -y

curl https://get.acme.sh | sh
```

## DNSPOD API授权
获取到`ID`和`Token`，然后执行下面设置环境变量
```sh
export DP_Id="IDxxxx"
export DP_Key="Tokenxxxx"
```

## 申请证书
```
~/.acme.sh/acme.sh --issue --dns dns_dp -d pouman.com -d *.pouman.com
```
Let’s Encrypt证书是三个月过期的，但你安装acme工具的时候，已经有加到定时刷新证书了。所以最好证书的路径不要改变。

## 下载证书
当上面的步骤搞完后，就等着邮件通知就OK了。证书就在那个管理页面下面下载即可。

