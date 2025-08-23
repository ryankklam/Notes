# NAS Setup Guide

## 配置源
docker HUB在中国被屏蔽了，需要其他外部源，但很多网上教程的源都不能连了 如163，alicloud等
参考这个链接找源。
现在配的源是[1ms](https://docker.1ms.run "1ms源")

[ref]: https://www.coderjia.cn/archives/dba3f94c-a021-468a-8ac6-e840f85867ea "目前国内可用Docker镜像源汇总（截至2025年6月）"

然后在container station里面存储库，添加一个新的库， 提供商选其他

docker exec -it 8efcb32255e /bin/bash

apt-get install -y dnsutils

拉取镜像以后，我们用浏览器访问一下，http://你的服务器IP：端口号，如果像下图一样返回就成功了。
{"data":{"app":"metatube","version":"v1.3.2-f2bbaee"}}

Jellyfin -
10222 -> 8086
http://192.168.1.174:10222/web/#/home.html

MetaTube -
10223 -> 8080
http://192.168.1.174:10223/

