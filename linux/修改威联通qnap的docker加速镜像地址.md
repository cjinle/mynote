# 修改威联通qnap的docker加速镜像地址

```sh
cd /share/CACHEDEV1_DATA/.qpkg/container-station/etc
vim docker.json # 看后下方的配置内容
/etc/init.d/container-station.sh restart
```

```json
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
```