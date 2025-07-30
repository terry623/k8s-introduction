---
theme: seriph
background: "./images/background.webp"
title: K8s Introduction
drawings:
  persist: false
transition: slide-left
mdc: true
---

# Kubernetes 新手指南
# 掌握核心概念快速入門

Terry Lin @MediaTek

---
layout: image-right
backgroundSize: 70%
image: /images/book.jpg
---

# 書籍介紹

## 從異世界歸來發現只剩自己不會 kubernetes

---
layout: image
backgroundSize: 80%
image: /images/deployment.png
---

# 網路部署的演變

---
layout: section
---

# 包含了哪些元件？

K8s 三兄弟 - Pod, Service, Deployment

---

# Pod

Pod 是 Node 中最小的單位，等於我們所使用的容器們都會被放置 Pod 裡管理

---

# Service

Service 定義『一群 Pod 要如何被連線及存取』 的元件
作為中介層，避免使用者和 Pod 進行直接連線

---
layout: image
backgroundSize: 80%
image: /images/deployment.png
---

# Deployment

Deployment 為 Pod 和 ReplicaSet 兩者提供了一個聲明式（declarative）定義的方法來達到使用者所期望的容器執行狀態

---

# Ingress

Ingress 將不同路徑的請求對應到各自的 Service，流量的負載均衡

---
layout: image
backgroundSize: 80%
image: /images/volume.png
---

# Volume

---

# ConfigMap & Secret

---

# Namespace

---

# OrbStack

---

# Lens