---
share: true
tags:
  - alist
  - webdav
title: window挂载webdav
date: 2023-11-19 12:54:37
update: 2023-11-19 01:07:37
---

在 `Windows` 中使用 `webdav` 挂载 `Alist` 的时候，始终无法成功：

![](/images/window挂载webdav_image_1.png)

![](/images/window挂载webdav_image_2.png)

在网上查找资料后知道 `windows` 中 `webdav` 客户端默认并没有开启对 `http` 协议支持，只能用 `https` 的协议，可以通过修改注册表开启 `http` 支持。

该配置在注册表中对应的地址为：`计算机\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters`，找到 `BasicAuthLevel` 把值由 `1` 改为 `2`。


![](/images/window挂载webdav_image_3.png)

之后重启 `WebClient` 服务即可：

![](/images/window挂载webdav_image_4.png)
