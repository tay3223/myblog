---
title: 修改Ingress的全局配置
date: 2021-02-08 13:06:39
tags:
---

### configmap可用参数列表（官方版）
```
https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/
```

### 解决400与414错误（他人博客）
```
https://www.cnblogs.com/malukang/p/12758802.html
```

### Ingress的常规操作
- 安装Ingress
- 修改Ingress的全局配置
- 创建Ingress与SLB的连接

### 主要参数
`client_header_buffer_size 1k`

`large_client_header_buffers 4 8k`

> 如果你的请求中的header都很大，那么应该使用client_header_buffer_size，这样能减少一次内存分配。

> 如果你的请求中只有少量请求header很大，那么应该使用large_client_header_buffers，因为这样就仅需在处理大header时才会分配更多的空间，从而减少无谓的内存空间浪费。

> 那么有人就会觉得奇怪了，为什么修改http header的大小就能解决get请求串过长的问题呢，这就要从http协议的get请求说起了，其实GET提交，请求的数据会附在URL之后（就是把数据放置在HTTP协议头中）。