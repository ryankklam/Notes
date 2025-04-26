# TroJan Guide

## 配置ec2 inbound rules ， 建议不要accept all traffic
##### IPv4	HTTPS	TCP	443	0.0.0.0/0
##### IPv4	HTTP	TCP	80	0.0.0.0/0
##### IPv4	SSH	    TCP	22	0.0.0.0/0

## 前置配置
去nameslio配置网址vs新ip



## EC2 trojan 安装

```shell
sudo -s ##切换超级用户
```shell

## 安装基础依赖
```shell
yum -y install wget    ##ContOS Yum 安装 wget
apt-get install wget   ##Debian Ubuntu 安装 wget
```shell

## 安装基础依赖
```shell
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan1.sh" && chmod +x trojan1.sh && ./trojan1.sh
```shell

## 更新账户邮箱
/root/.acme.sh/acme.sh --register-account -m ryan4299899@gmail.com

## 申请证书
```shell
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan2.sh" && chmod +x trojan2.sh && ./trojan2.sh
```shell


可能会遇到acme申请证书不成功的情况，log有提示是 “Please update your account with an email address first.”
[Sun Apr 23 04:23:37 UTC 2023] Installing from online archive.
[Sun Apr 23 04:23:37 UTC 2023] Downloading https://github.com/acmesh-official/acme.sh/archive/master.tar.gz
[Sun Apr 23 04:23:38 UTC 2023] Extracting master.tar.gz
[Sun Apr 23 04:23:38 UTC 2023] Installing to /root/.acme.sh
[Sun Apr 23 04:23:38 UTC 2023] Installed to /root/.acme.sh/acme.sh
[Sun Apr 23 04:23:38 UTC 2023] Installing alias to '/root/.bashrc'
[Sun Apr 23 04:23:38 UTC 2023] OK, Close and reopen your terminal to start using acme.sh
[Sun Apr 23 04:23:38 UTC 2023] Installing cron job
48 0 * * * "/root/.acme.sh"/acme.sh --cron --home "/root/.acme.sh" > /dev/null
[Sun Apr 23 04:23:38 UTC 2023] Good, bash is found, so change the shebang to use bash as preferred.
[Sun Apr 23 04:23:38 UTC 2023] OK
[Sun Apr 23 04:23:38 UTC 2023] Install success!
[Sun Apr 23 04:23:39 UTC 2023] Using CA: https://acme.zerossl.com/v2/DV90
[Sun Apr 23 04:23:40 UTC 2023] No EAB credentials found for ZeroSSL, let's get one
[Sun Apr 23 04:23:40 UTC 2023] acme.sh is using ZeroSSL as default CA now.
[Sun Apr 23 04:23:40 UTC 2023] Please update your account with an email address first.
[Sun Apr 23 04:23:40 UTC 2023] acme.sh --register-account -m my@example.com


需要执行
/root/.acme.sh/acme.sh --register-account -m ryan4299899@gmail.com


## BBR加速
```shell
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan3.sh" && chmod +x trojan3.sh && ./trojan3.sh
```shell

======================请详细阅读下面的说明========================
==================================================================
Chrome浏览器地址栏前面若没有小锁，Trojan服务绝对不成功
Chrome浏览器若是有小锁，Trojan服务绝对正常
若是客户端不能连接Trojan,请尝试重启Trojan服务
Trojan服务重启命令：systemctl restart trojan
==================================================================
==================================================================
你的Trojan配置信息存放在：/usr/local/etc/trojan/配置.txt
==================================================================
==================================================================
