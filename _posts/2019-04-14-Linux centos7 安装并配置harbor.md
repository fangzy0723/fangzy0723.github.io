

#### Linux centos7 安装并配置harbor

1、下载安装包[下载地址](https://storage.googleapis.com/harbor-releases/release-1.7.0/harbor-offline-installer-v1.7.5.tgz)

2、上传到服务器上指定位置如/apps，执行解压缩命令
```
tar -zxvf harbor-offline-installer-v1.7.5.tgz
cd harbor/
```
3、可以看到harbor.cfg配置文件，修改hostname
```
hostname = hub.fangzy.me
```
4、配置insecure-registry 指定私有仓库地址
```
vim /etc/docker/daemon.json 
```
添加如下内容
```
{
"insecure-registries" : ["hub.fangzy.me"]
}
```
5、配置hosts文件
```
vim /etc/hosts
```
添加如下内容
```
106.13.97.78 hub.fangzy.me
```
6、重启docker
```
systemctl daemon-reload
systemctl restart docker
```
7、启动harbor,在harbor下执行如下命令
```
./prepare
./install.sh 
```
8、打镜像tag，如下所示
```
docker tag goharbor/nginx-photon:v1.7.5 hub.fangzy.me/test/db:v1.1
```
9、push镜像到harbor需要先登录
```
执行 docker login hub.fangzy.me
输入账号：admin
输入密码：Harbor12345

[root@instance-qntpnk4r harbor]# docker login hub.fangzy.me
Username: admin
Password: 
Login Succeeded
输出Login Succeeded说明登录成功
```
10.push镜像到harbor
```
docker push images:tag

[root@instance-qntpnk4r harbor]# docker push hub.fangzy.me/test/db:v1.1
The push refers to a repository [hub.fangzy.me/test/db]
e95514e23db7: Layer already exists 
f60840e24dbf: Layer already exists 
v1.2: digest: sha256:17acf142e008123739833aac80c9c39ec2ff86d79d22e16d25bb87be03ea01cb size: 739
```
至此上传镜像到harbor成功


