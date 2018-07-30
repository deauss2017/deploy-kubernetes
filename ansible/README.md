选自：https://github.com/kubernetes-incubator/kubespray

安装依赖工具

yum install epel-release -y

yum update

yum install git python python-pip -y
安装ansible

国内普通安装
#pip install pip --upgrade
#pip install ansible

使用阿里云加速安装ansible
pip install pip --upgrade -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
pip install --no-cache-dir ansible -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
服务器的基本设置

升级内核
ssh免秘钥访问
ssh-keygen -t rsa -b 2048 回车 回车 回车
ssh-copy-id
时间一致
使用date命令查看 修改时间：
date -s  "2018-5-30 14:21:00"
修改时区：

cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
安装kubernetes集群

初始化git目录

git init
将ansible的kubernetes项目拉取下来

git clone https://github.com/gjmzj/kubeasz.git
创建ansible目录并将拉取下来的文件移动到目录里

mkdir -p /etc/ansible
mv kubeasz/* /etc/ansible
下载kubernetes的版本源码包

https://kubernetes.io/docs/imported/release/notes/#client-binaries
或是在百度网盘上

链接：https://pan.baidu.com/s/1i9idEc79hHRSwGXcO0SS9A 
密码：gy96
解压源码包

tar zxvf k8s.193.tar.gz
mv bin/* /etc/ansible/bin
通过模板创建hosts文件

cd /etc/ansible
cp example/hosts.allinone.example hosts
模板地址 ./example/

单节点部署
hosts.allinone.example
多主多节点
hosts.m-masters.example
单主多节点
hosts.s-master.example
A
B
How are you?
Great!
A
B
模板hosts地址

http://note.youdao.com/noteshare?id=a782ec11cd6cb83100898ac6326ae877&sub=92788436400F4F89B3E56AC64B1F6B76
ansible部署kubernetes

ansible-playbook 90.setup.yml
或是
单个执行
ansible-playbook 01.prepare.yml
安装完成后 命令不能用，退出shell重新进入

查看集权状态

安装组件

/etc/ansible/manifests/目录下
kubectl apply -f *.yaml

清理集群

ansible-playbook 99.clean.yml
