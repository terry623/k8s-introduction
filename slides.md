---
theme: seriph
background: "/images/background.webp"
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

### 從異世界歸來發現只剩自己不會 Kubernetes

<br/>

- K8s 已成為現代雲端與容器化部署的主流技術
- 企業、開發者、DevOps 團隊都在學習與導入
- 本簡報將帶你從零開始，掌握 K8s 的核心概念

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

---

# Pod

Pod 是 Kubernetes 中最小的可部署單位，通常包含一個或多個容器。

- 每個 Pod 會被部署在某個 Node 上
- Pod 內的容器共享網路與儲存空間
- 適合部署緊密耦合的應用（如主程式+sidecar）
- Pod 生命週期短暫，通常由 Deployment 等控制器管理

---

# Service

Service 定義一組 Pod 的存取方式，提供穩定的網路入口。

- 解決 Pod IP 會變動的問題
- 支援負載均衡，將流量分配到多個 Pod
- 常見類型：ClusterIP（內部）、NodePort（外部）、LoadBalancer（雲端）

- Service 是用戶端與 Pod 之間的中介層，避免直接連線 Pod

---

# Deployment

Deployment 提供聲明式（declarative）方式管理 Pod 與 ReplicaSet。

- 可自動建立、更新、回滾 Pod
- 支援彈性擴展（水平擴展/縮減）
- 維持應用程式高可用性

- 實務上，幾乎所有應用都建議用 Deployment 來管理
---

# Ingress

Ingress 提供 HTTP/HTTPS 路由，將外部請求導向不同的 Service。

- 支援路徑、主機名稱等多種規則
- 可整合 TLS，實現 HTTPS
- 常用於微服務架構下的 API Gateway

- Ingress Controller（如 NGINX Ingress）需額外安裝

---

# Volume

Volume 提供 Pod 持久化儲存空間。

- 解決容器重啟資料遺失問題
- 支援多種後端（本地磁碟、NFS、雲端儲存等）
- 常見類型：emptyDir、hostPath、PersistentVolume（PV）、PersistentVolumeClaim（PVC）

---

# ConfigMap & Secret

ConfigMap 與 Secret 用於管理應用程式設定與敏感資訊。

- **ConfigMap**：儲存非敏感設定（如環境變數、組態檔）
- **Secret**：儲存密碼、API 金鑰等敏感資料（Base64 編碼）

- 可將 ConfigMap/Secret 掛載為環境變數或檔案

---

# Namespace

Namespace 用於資源隔離與多租戶管理。

- 預設有 default、kube-system、kube-public 等
- 適合大型團隊、不同專案或環境（dev/stage/prod）隔離
- 可限制資源配額（ResourceQuota）

---
layout: section
---

# 相關工具介紹

---

# OrbStack

OrbStack 是一款輕量級本地容器與虛擬機管理工具。

- 支援快速建立 K8s 測試環境
- 介面簡單易用，適合開發者本機測試
- 可與 Docker Desktop、Minikube 等工具互補

**優點：**
- 啟動速度快、資源佔用低
- 支援多平台（macOS、Windows）

---

# Lens

Lens 是一款開源的 Kubernetes 圖形化管理工具。

- 提供直觀的 UI，方便瀏覽叢集資源、監控狀態
- 支援多叢集管理、即時日誌、資源編輯
- 適合新手與進階用戶快速上手 K8s

**特色：**
- 一鍵連線多個 K8s 叢集
- 內建資源圖表、事件追蹤
- 支援 Marketplace 擴充功能

---
layout: statement
---

<img src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExaWF4eDVrdjdsbnFsaThkNG01NGNucGNlYWc2c2JxdTc2cm5zMjY3ZSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ZfK4cXKJTTay1Ava29/giphy.gif" width="50%" style="display: block; margin: 0 auto;"/>