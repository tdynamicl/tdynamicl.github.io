---
title: 修改k8s的nodeport限制
date: 2025-04-24 18:51:16
tags:
---

![](/images/4164cff8-9750-4f4d-bf9b-3c430756a554.png)

在k8s的master节点上编辑：`/etc/kubernetes/manifests/kube-apiserver.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  annotations:
    scheduler.alpha.kubernetes.io/critical-pod: ""
  creationTimestamp: null
  labels:
    component: kube-apiserver
    tier: control-plane
  name: kube-apiserver
  namespace: kube-system
spec:
  containers:
  - command:
    - kube-apiserver
    # ...
    # 本次添加的选项，用于修改nodeport范围
    – --service-node-port-range=1-65535

```

