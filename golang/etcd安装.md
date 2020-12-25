# etcd安装

## 下载
[github](https://github.com/etcd-io/etcd)

## 安装 
```shell
mkdir -p /opt/soft/etcd
tar xvf xxx.tar.gz -C /opt/soft/etcd
```

## 单台配置
```shell
name: "default"
listen-client-urls: "http://192.168.122.1:2379"
advertise-client-urls: "http://192.168.122.1:2379"
```
[配置样例](https://github.com/etcd-io/etcd/blob/master/etcd.conf.yml.sample)

## 集群

###  etcd0
```yaml
name: "etcd0"
listen-peer-urls: "http://192.168.122.1:2380"
listen-client-urls: "http://192.168.122.1:2379"

initial-advertise-peer-urls: "http://192.168.122.1:2380"
advertise-client-urls: "http://192.168.122.1:2379"

initial-cluster: "etcd0=http://192.168.122.1:2380,etcd1=http://192.168.122.242:2380,etcd2=http://192.168.122.231:2380"
initial-cluster-token: "etcd-cluster"
initial-cluster-state: "existing"
```

### etc1
```yaml
listen-peer-urls: "http://192.168.122.242:2380"
listen-client-urls: "http://192.168.122.242:2379"

initial-advertise-peer-urls: "http://192.168.122.242:2380"
advertise-client-urls: "http://192.168.122.242:2379"

initial-cluster: "etcd0=http://192.168.122.1:2380,etcd1=http://192.168.122.242:2380,etcd2=http://192.168.122.231:2380"
initial-cluster-token: "etcd-cluster"
initial-cluster-state: "new"

```

### etc2
```yaml
name: "etcd2"
listen-peer-urls: "http://192.168.122.231:2380"
listen-client-urls: "http://192.168.122.231:2379"

initial-advertise-peer-urls: "http://192.168.122.231:2380"
advertise-client-urls: "http://192.168.122.231:2379"

initial-cluster: "etcd0=http://192.168.122.1:2380,etcd1=http://192.168.122.242:2380,etcd2=http://192.168.122.231:2380"
initial-cluster-token: "etcd-cluster"
initial-cluster-state: "new"
```
