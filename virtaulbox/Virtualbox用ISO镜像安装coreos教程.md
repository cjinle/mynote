# virtualbox用ISO镜像安装coreos教程

### 1. 下载引导安装ISO文件

下载地址：[coreos_production_iso_image.iso](https://stable.release.core-os.net/amd64-usr/current/coreos_production_iso_image.iso)

### 2. virtualbox挂载ISO镜像启动


### 3. 生成SSH登录密钥
```bash
$ ssh-keygen -t rsa
```

### 4. 准备安装配置cloud-config.yaml
```yaml
hostname: coreos
coreos:
        units:
                - name: etcd2.service
                  command: start
                - name: fleet.service
                  command: start
        etcd2:
          discovery: https://discovery.etcd.io/cb33f38c16bead3a376be9bfc706987
          advertise-client-urls: http://$private_ipv4:2379,http://$private_ipv4:4001
          initial-advertise-peer-urls: http://$private_ipv4:2380
          listen-client-urls: http://0.0.0.0:2379,http://0.0.0.0:4001
          listen-peer-urls: http://$private_ipv4:2380,http://$private_ipv4:7001
        fleet:
          metadata: role=coreos01
users:
        - name: core
          ssh-authorized-keys:
                - ssh-rsa xxxxxxxxxxxxxxxxxxx
        - groups:
               - sudo
               - docker
```

### 5. 准备安装时需要的镜像bin(防止网络不稳定)，需要自己搭建HTTP服务器

 - [coreos_production_image.bin.bz2](http://stable.release.core-os.net/amd64-usr/current/coreos_production_image.bin.bz2)
 - [coreos_production_image.bin.bz2.sig](http://stable.release.core-os.net/amd64-usr/current/coreos_production_image.bin.bz2.sig)


### 6. 安装脚本执行

```bash
$ coreos-install -d /dev/sda -c cloud-config.yaml -b http://192.168.2.100/
```

### 7. 记得复制生成SSH密钥，因为coreos只能用这个登录

### 8. 安装完毕，重启虚拟机，配置163源
```bash
echo 'DOCKER_OPTS="--registry-mirror=http://hub-mirror.c.163.com"' >> /run/flannel_docker_opts.env
```
