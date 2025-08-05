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

<!--
很新手的 K8s 的分享，如果講錯或覺得欸 Terry 根本在亂講
歡迎直接指正我這樣
-->

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

<!--
之前在處理 AIH 的專案時，有碰到蠻多 Deployment 的問題
所以後來買了本書來看了一下
-->

---
layout: image
backgroundSize: 80%
image: /images/deployment.png
---

# 網路部署的演變

<!--
傳統部署 (Traditional)
做法：直接把應用裝在實體伺服器上。
優缺點：效能接近裸機，簡單易懂；但伺服器閒置率高，擴充與隔離能力差。

因此人們開始思考是否能在同一台物理伺服器上使用虛擬的隔離技術。

虛擬化部署 (Virtualized)
做法：在實體機跑 Hypervisor，建立多個具備完整 OS 的 VM。
優缺點：資源隔離佳、可做快照與搬遷；但每台 VM 含完整 OS，開銷大、啟動慢。

容器化部署 (Container)
做法：以容器共享主機核心，只打包應用與函式庫。
優缺點：啟動秒級、資源輕量、一致性高；但隔離不及 VM，需要額外工具管理。
-->

---

# 為何要用 Kubernetes？

- **自動化與高可靠性**：自動部署、擴展、修復，確保服務穩定不中斷。
- **彈性擴展與資源最佳化**：根據需求動態調整資源，提升硬體利用率。
- **跨平台一致性**：支援本地、雲端與多雲環境，部署流程一致。

<br/>

> Kubernetes 幫助團隊提升效率、穩定性與彈性，是現代雲端架構的關鍵基石。

<!--
「首先是自動化與高可靠性。想像一下，你的服務半夜突然掛了，K8s 能像個盡責的警衛，自動偵測到問題，然後重新啟動一個新的實例來取代它，整個過程完全自動化，確保服務不中斷。」

「再來是彈性擴展與資源最佳化。當你的網站流量突然暴增，比如在辦促銷活動時，K8s 可以自動增加服務的副本數量來應對；流量高峰過了，它又會自動縮減，這樣不僅能應付高併發，還能最大化硬體資源的利用率，幫你省錢。」

「最後是跨平台一致性。無論你是在自己的筆電上、公司的機房，還是在 AWS、Google Cloud 這種公有雲上，K8s 都提供了一致的部署和管理體驗。開發人員在本機測試好的東西，可以無痛地部署到生產環境。」
-->

---
layout: section
---

# 核心概念

---

# Cluster

*Cluster 就像一座「雲端城市」，由多棟大樓（Node）組成，透過道路（網路）連接，並有市政府（Control Plane）統籌規劃。*

Cluster 是由一組機器（實體或虛擬）組成的集合，這些機器共同協作來執行與管理容器化應用程式。

- 一個叢集至少包含一個 Control Plane（控制平面）與多個 Node（工作節點）
- 控制平面負責整體調度、管理與監控
- Node 負責實際執行應用程式容器
- 叢集設計可擴展、高可用，適合大規模部署

---

# Control Plane（控制平面）

*Control Plane 就像「市政府」，負責整個城市的規劃、調度與監管。*

Control Plane（控制平面）是 Kubernetes 叢集的核心大腦，負責協調、調度與管理所有 Node 和應用程式。

- 負責資源調度、狀態監控、生命週期管理
- 接收用戶指令，決定如何分配工作到各個 Node

---

# Node

*Node 就像城市裡的一棟大樓，裡面有電力、網路、空調，讓公司（Pod）進駐。*

Node 是 Kubernetes 叢集中的一台伺服器（可為實體機或虛擬機），負責執行 Pod 與容器。

- 每個 Node 會安裝 kubelet、容器執行環境（如 containerd、Docker）
- Node 會接收控制平面的指令，負責資源分配與容器管理
- 一個叢集可包含多個 Node，實現負載分散與高可用
- Node 故障時，Kubernetes 會自動將工作移轉到其他健康節點

---
layout: image
backgroundSize: 50%
image: /images/structure.png
---

---

# Pod

*Pod 就像公司租的「套房單位」，一個或多個容器住在同一房間，共用門牌（IP）和客廳（Storage、Network Namespace）。*

Pod 是 Kubernetes 中最小的可部署單位，通常包含一個或多個容器。

- 每個 Pod 會被部署在某個 Node 上
- 每個容器對應一個 Image
- Pod 內的容器共享網路與儲存空間
- 適合部署緊密耦合的應用（如主程式+sidecar）
- Pod 生命週期短暫，通常由 Deployment 等控制器管理

---

# Service

*Service 就像城市的「統一服務櫃檯」，不論背後有幾家分店（Pod），外界都只記櫃檯電話。*

Service 定義一組 Pod 的存取方式，提供穩定的網路入口。

- 解決 Pod IP 會變動的問題
- 支援負載均衡，將流量分配到多個 Pod
- 常見類型：ClusterIP（內部）、NodePort（外部）、LoadBalancer（雲端）

- Service 是用戶端與 Pod 之間的中介層，避免直接連線 Pod

---

# Deployment

*Deployment 就像連鎖餐廳的「建案藍圖」，標準化複製分店，倒一家會自動補蓋同規格的新店。*

Deployment 提供聲明式（declarative）方式管理 Pod 與 ReplicaSet。

- 可自動建立、更新、回滾 Pod
- 支援彈性擴展（水平擴展/縮減）
- 維持應用程式高可用性

- 實務上，幾乎所有應用都建議用 Deployment 來管理
---

# Ingress

*Ingress 就像城市入口的「高速公路收費站」，根據路徑或子網域把車流導向對應服務台，並可設 SSL、驗證等安全措施。*

Ingress 提供 HTTP/HTTPS 路由，將外部請求導向不同的 Service。

- 支援路徑、主機名稱等多種規則
- 可整合 TLS，實現 HTTPS
- 常用於微服務架構下的 API Gateway

- Ingress Controller（如 NGINX Ingress）需額外安裝

---

# Volume

*Volume 就像公司套房裡的「保險箱」或「儲藏室」，讓資料不會因搬家（重啟）而遺失。*

Volume 提供 Pod 持久化儲存空間。

- 解決容器重啟資料遺失問題
- 支援多種後端（本地磁碟、NFS、雲端儲存等）
- 常見類型：emptyDir、hostPath、PersistentVolume（PV）、PersistentVolumeClaim（PVC）

---

# ConfigMap & Secret

*ConfigMap 是公開說明書，Secret 是機密檔案，都是掛在 Pod 裡的「文件櫃」；前者可上公告欄，後者必須上鎖。*

ConfigMap 與 Secret 用於管理應用程式設定與敏感資訊。

- **ConfigMap**：儲存非敏感設定（如環境變數、組態檔）
- **Secret**：儲存密碼、API 金鑰等敏感資料（Base64 編碼）

- 可將 ConfigMap/Secret 掛載為環境變數或檔案

---
layout: section
---

# 相關工具介紹

---

# [OrbStack](https://orbstack.dev/)

OrbStack 是一款輕量級本地容器與虛擬機管理工具。

- 支援快速建立 K8s 測試環境
- 介面簡單易用，適合開發者本機測試
- 可與 Docker Desktop、Minikube 等工具互補

**優點：**
- 啟動速度快、資源佔用低
- 支援多平台（macOS、Windows）

---

# [Lens](https://k8slens.dev/)

Lens 是一款開源的 Kubernetes 圖形化管理工具。

- 提供直觀的 UI，方便瀏覽叢集資源、監控狀態
- 支援多叢集管理、即時日誌、資源編輯
- 適合新手與進階用戶快速上手 K8s

**特色：**
- 一鍵連線多個 K8s 叢集
- 內建資源圖表、事件追蹤
- 支援 Marketplace 擴充功能

---
layout: section
---

# Demo: How to Deploy AI Hub

---
layout: statement
---

<img src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExaWF4eDVrdjdsbnFsaThkNG01NGNucGNlYWc2c2JxdTc2cm5zMjY3ZSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ZfK4cXKJTTay1Ava29/giphy.gif" width="50%" style="display: block; margin: 0 auto;"/>
