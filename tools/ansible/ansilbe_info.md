# 奇点系统ansible运维操作手册

[TOC]

## ansible架构

![](http://getansible.com/architecture/ansible-multiple-machine-edited.png)

## 为什么要用ansible
解决IT自动化问题，减少人工操作批量任务的劳动和出错概率，在一定程度上可以代替IT操作文档。在机器迁移和重新部署阶段也可以节约大量工作。总之ansible可以减少而非增多我们ops方面的工作。

ansible已经被红帽收购，支持方面不成问题，目前的module已经有数百个，包括AWS、Docker均有良好支持。且ansible相对同类组件的优点是不需要在目标服务器上安装客户端，仅通过ssh进行通信，完全符合目前公司和大多数云环境的要求。

## 添加ssh

中控机：10.153.61.168
密码：自行登录roc查看

在申请完业务虚机后，执行如下命令向业务机添加中控机ssh公钥

```
ssh-keygen
ssh-copy-id -i ~/.ssh/id_rsa.pub root@10.152.46.226
ssh-keyscan 10.152.46.226 >> ~/.ssh/known_hosts
```

其中ssh-keygen仅在中控机没有生成过公钥的情况下需要执行一次，后续复用即可，10.153.61.168无需再次执行。

ssh-copy-id的过程中需要输入一次目标机的密码。

ssh-keyscan可以一次输入多个ip，用空格隔开。

## ansible项目

https://git.sogou-inc.com/adstream/ansible_playbooks

## 执行方式

进入中控机/search/odin/ansible_playbooks目录

目前支持的操作

安卓jenkins机器公钥(hosts group=ssh)

```
ansible-playbook -i hosts playbook-jenkins_ssh.yml
```

安装jdk(hosts group=java)

```
ansible-playbook -i hosts playbook-java.yml
```

安装openresty(hosts group=openresty)

```
ansible-playbook -i hosts playbook-openresty.yml
```

安装nexus(hosts group=nexus)

```
ansible-playbook -i hosts playbook-nexus.yml
```

安装logstash(hosts group=logstash)

```
ansible-playbook -i hosts playbook-logstash.yml --extra-vars "env=dev"
```

env支持dev和prod，对应的配置分别放在roles=logstash的vars目录下

安装通用java环境

```
ansible-playbook -i hosts playbook-qd-general.yml --extra-vars "var_hosts=portal-mix-dev"
```

其中portal-mix-dev是hosts文件中要部署的机器组名，目标机器要申请NAT权限。

以下再贴几个ansible shell

复制文件

```
ansible test -m copy -a "src=~/dump.rdb dest=/tmp" -u root
```

删除文件

```
ansible test -m file -a "path=/tmp/dump.rdb state=absent" -u root
```

## 参考资料

电子书 http://getansible.com

module大全 http://docs.ansible.com/ansible/latest/list_of_all_modules.html

ansible galaxy(他人共享的现成脚本) https://galaxy.ansible.com

入门教程（强烈推荐观看）https://www.ansible.com/resources/webinars-training/introduction-to-ansible

