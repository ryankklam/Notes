# TroJan Guide

## ����ec2 inbound rules �� ���鲻Ҫaccept all traffic
##### IPv4	HTTPS	TCP	443	0.0.0.0/0
##### IPv4	HTTP	TCP	80	0.0.0.0/0
##### IPv4	SSH	    TCP	22	0.0.0.0/0

## ǰ������
ȥnameslio������ַvs��ip



## EC2 trojan ��װ

```shell
sudo -s ##�л������û�
```shell

## ��װ��������
```shell
yum -y install wget    ##ContOS Yum ��װ wget
apt-get install wget   ##Debian Ubuntu ��װ wget
```shell

## ��װ��������
```shell
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan1.sh" && chmod +x trojan1.sh && ./trojan1.sh
```shell

## �����˻�����
/root/.acme.sh/acme.sh --register-account -m ryan4299899@gmail.com

## ����֤��
```shell
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan2.sh" && chmod +x trojan2.sh && ./trojan2.sh
```shell


���ܻ�����acme����֤�鲻�ɹ��������log����ʾ�� ��Please update your account with an email address first.��
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


��Ҫִ��
/root/.acme.sh/acme.sh --register-account -m ryan4299899@gmail.com


## BBR����
```shell
wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan3.sh" && chmod +x trojan3.sh && ./trojan3.sh
```shell

======================����ϸ�Ķ������˵��========================
==================================================================
Chrome�������ַ��ǰ����û��С����Trojan������Բ��ɹ�
Chrome�����������С����Trojan�����������
���ǿͻ��˲�������Trojan,�볢������Trojan����
Trojan�����������systemctl restart trojan
==================================================================
==================================================================
���Trojan������Ϣ����ڣ�/usr/local/etc/trojan/����.txt
==================================================================
==================================================================
