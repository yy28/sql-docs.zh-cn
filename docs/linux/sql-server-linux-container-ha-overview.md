---
title: SQL Server 容器的高可用性
description: 本文介绍 SQL Server 容器的高可用性
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: aa54849c16ea9dfb821404b553b1e9183b61d66a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077482"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server 容器的高可用性

在 Kubernetes 中本机创建和管理 SQL Server 实例。

将 SQL Server 部署到由 [Kubernetes](https://kubernetes.io/) 管理的 Docker 容器。 在 Kubernetes 中，具有 SQL Server 实例的容器可以在群集节点出现故障时自动进行恢复。 为实现更可靠的可用性，请使用 Kubernetes 群集上容器中的 SQL Server 实例来配置 SQL Server Always On 可用性组。 本文将比较两种解决方案。

## <a name="compare-sql-server-versions-on-kubernetes"></a>比较 Kubernetes 上的 SQL Server 版本

SQL Server 2017 提供可以在 Kubernetes 上部署的 Docker 映像。 可以使用 Kubernetes 持久卷声明 (PVC) 来配置映像。 Kubernetes 监视容器中的 SQL Server 进程。 如果进程、Pod、容器或节点发生故障，Kubernetes 将自动启动另一个实例，并重新连接到存储。

SQL Server 2019（预览版）使用 Kubernetes StatefulSet 引入了更可靠的体系结构。 容器映像参与 SQL Server Always On 可用性组，而 Kubernetes 在这些容器映像中协调 SQL Server 实例。 此模式提供了改进后的运行状况监视、更快恢复、卸载备份和读取横向扩展。  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Kubernetes 上存在具有 SQL Server 实例的容器

Kubernetes 1.6 及更高版本支持[存储类](https://kubernetes.io/docs/concepts/storage/storage-classes/)、[持久卷声明](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)和 [Azure 磁盘卷类型](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)    。 

在此配置中，Kubernetes 扮演容器业务流程协调程序一角。 

![Kubernetes SQL Server 群集示意图](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上图中，`mssql-server` 是 [Pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/) 中的 SQL Server 实例（容器）  。 [副本集](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可确保在节点发生故障后自动恢复 Pod。 应用程序连接到服务。 在这种情况下，该服务表示负载均衡器，承载着 `mssql-server` 发生故障后保持不变的 IP 地址。

Kubernetes 协调群集中的资源。 如果承载 SQL Server 实例容器的节点发生故障，该节点会使用 SQL Server 实例来启动新容器，并将其附加到同一个持久存储上。

SQL Server 2017 及更高版本支持 Kubernetes 上的容器。

若要在 Kubernetes 中创建容器，请查看[在 Kubernetes 中部署 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Kubernetes 中 SQL Server 容器上的 SQL Server Always On 可用性组

SQL Server 2019 支持 Kubernetes 中容器上的可用性组。 对于可用性组，将 SQL Server [Kubernetes 运算符](https://coreos.com/blog/introducing-operators.html)部署到 Kubernetes 群集。 运算符有助于打包、部署和管理群集中的 SQL Server 实例和可用性组。

![Kubernetes 容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上图中，四节点的 Kubernetes 群集承载着具有三个副本的可用性组。 此解决方案包括以下组件：

* 一个 Kubernetes [部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)  。 该部署包括运算符和配置映射。 该部署描述了为可用性组部署 SQL Server 实例所需的容器映像、软件和说明。

* 三个节点，每个节点都承载一个 [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)  。 StatefulSet 包含一个 Pod。 每个 Pod 都包含以下内容：
  * 运行 SQL Server 实例的 SQL Server 容器。
  * 管理可用性组的超级用户 `mcr.microsoft.com/mssql/ha`。

* 与可用性组相关的两个 [ConfigMaps](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)  。 ConfigMaps 提供以下信息：
  * 运算符的部署。
  * 可用性组。

 * 每个 SQL Server 实例的持久卷为数据和日志文件提供存储。

此外，群集还存储密码、证书、密钥和其他敏感信息等的[机密](https://kubernetes.io/docs/concepts/configuration/secret/)  。

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>比较包含/未包含可用性组的容器上的 SQL Server 高可用性

下表比较了包含/未包含可用性组的 Kubernetes 上容器中的 SQL Server 高可用性功能：

| |包含可用性组 | 独立容器实例<br/> 未包含可用性组
|:------|:------|:------
|从节点故障中自动恢复 | 是 | 是
|从 Pod 故障中自动恢复 | 是 | 是
|故障转移速度更快 |是 |
|从 SQL Server 实例故障中自动恢复 | 是 | 
|从数据库运行状况检查故障中自动恢复 | 是 | 
|提供只读副本 | 是 |
|次要副本备份 | 是 | 
|作为 StatefulSet 运行 | 是 | 

关键区别在于，使用可用性组的恢复（或故障转移）时间比使用一个容器中的 SQL Server 实例更快。 这一改进的原因在于，SQL Server 可用性组会在群集中的其他节点上保留次要副本。 进行故障转移时，选择次要副本并将其提升为主要副本。 连接到服务的应用程序将重新定向到新的主要副本。

在没有可用性组的情况下，如果 Kubernetes 检测故障转移，则需要创建容器，将其连接到存储，然后再重新连接那些连接到服务的应用程序。 精确的故障转移时间取决于故障转移位置以及检测方式。 

通常情况下，可用性组的故障转移时间以秒为单位进行测量，而用于恢复容器的单个实例的故障转移时间最长可达 10 分钟。

## <a name="next-steps"></a>后续步骤

若要在 Azure Kubernetes Service (AKS) 中部署 SQL Server 容器，请参阅以下示例：

* [在 Docker 容器中部署 SQL Server](sql-server-linux-configure-docker.md)
* [在 Kubernetes 中部署 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
* [SQL Server 容器的 Always On 可用性组](sql-server-ag-kubernetes.md)

