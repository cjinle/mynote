# docker入门



## 常用命令
```shell
sudo docker ps           # 列出当前运行的docker程序 
sudo docker ps -a        # 列出所有docker程序 

sudo docker images       # 列出所有本地docker镜像 

sudo docker ps -qa       # 列出所有docker程序的ID
sudo docker images -qa   # 列出所有docker镜像的ID

sudo docker rm -f $(sudo docker ps -qa)  # 删除所有docker程序
sudo docker rmi -f $(sudo docker ps -qa) # 删除所有docker镜像 


sudo docker save chenjinle/ip2region:latest -o ip2region.tar  # 本地仓库镜像导出
sudo docker load ip2region.tar   # 加载本地文件到仓库镜像  
```
