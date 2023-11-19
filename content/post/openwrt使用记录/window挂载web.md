---
share: true
tags:
  - alist
  - "#webdav"
title: window挂载web
date:  2023-11-19 12:54:37
update:  2023-11-19 12:19:22
---
在 `Windows` 中使用 `webdav` 挂载 `Alist` 的时候，始终无法成功

![](/images/IMG-window挂载web-20231119005454824.png)

![](/images/IMG-window挂载web-20231119005507621.png)

在网上查找资料后知道 `windows` 中 `webdav` 客户端默认并没有开启对 `http` 协议支持，只能用 `https` 的协议，可以通过修改注册表开启 `http` 支持。

该配置在注册表中对应的地址为：`计算机\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters`，找到 `BasicAuthLevel` 把值由 `1` 改为 `2`。

![image-20230311101002963](https://git.mengqingpo.com:8888//fugary/blogpic/uploads/ab9e7b7d701010cf6e42a6f356fe3ea0/image-20230311101002963.png)

之后重启 `WebClient` 服务即可：

![image-20230311101203216](https://git.mengqingpo.com:8888//fugary/blogpic/uploads/ad6e819d374a5ac3c79441ac134193c3/image-20230311101203216.png)
