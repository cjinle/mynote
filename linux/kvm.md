# ubuntu install kvm



## download

## install  

## 管理 
```sh
virsh list --all
virsh start centos7.0
virsh shutdown centos7.0
```

## clone


```sh
sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
```

## network

```sh
apt-get install bridge-utils
brctl show virbr0
virsh domiflist centos7.0 # 查看虚拟网卡信息

arp -n
```

