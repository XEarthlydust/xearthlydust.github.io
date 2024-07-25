---
title: 记录一次学习K8S Gateway的部署
date: 2024-07-25 14:27:21
tags:
---
### 前言
粗浅学习了K8S相关的东西，国内的资源时效性还是落后一些，记录一下Gateway的部署流程，备忘笔记。

### 安装 Gateway API CRD
[官方文档](https://kubernetes.io/zh-cn/docs/concepts/services-networking/gateway/)
K8S默认没有对 Gateway API 资源进行实现，需要手动进行CRD (Custom Resource Definition)
[关于安装CRDs](https://gateway-api.sigs.k8s.io/guides/#installing-gateway-api)
```bash
# Install Standard Channel
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.1.0/standard-install.yaml

# Install Experimental Channel
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.1.0/experimental-install.yaml
```
### 选择合适的 Gateway Controller 实现
懵，东西好多，看有一部分资源教程是用 `Istio` ，我还是选择 `NGINX Gateway Fabric` (nginx 老熟人了)吧
[实现列表](https://gateway-api.sigs.k8s.io/implementations/)
[入门指南]()