---
title: 运行 Linux 的容器的 Always On 可用性组
titleSuffix: SQL Server
description: 本文介绍 SQL Server 容器上的可用性组
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3910c74be803b7fc63c8bf560fc637387e06ee15
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910471"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>SQL Server 容器的 AlwaysOn 可用性组

SQL Server 2019 支持 Kubernetes 群集中容器上的可用性组。 对于可用性组，将 SQL Server [Kubernetes 运算符](https://coreos.com/blog/introducing-operators.html)部署到 Kubernetes 群集。 运算符有助于打包、部署和管理群集中的可用性组。

![Kubernetes 容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上图中，四节点的 kubernetes 群集托管具有三个副本的可用性组。 此解决方案包含以下组件：

* Kubernetes [部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)  。 部署包含运算符和配置映射。 它们提供为可用性组部署 SQL Server 实例所需的容器映像、软件和说明。

* 三个节点，每个节点都托管一个 [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)  。 StatefulSet 包含一个 [pod](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)  。 每个 pod 包含：
  * 运行 SQL Server 实例的 SQL Server 容器。
  * 可用性组代理。 

* 与可用性组相关的两个 [ConfigMaps](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)  。 ConfigMaps 提供以下信息：
  * 运算符的部署。
  * 可用性组。

 * [永久性卷](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)是一系列存储区  。 永久性卷声明 (PVC) 是指用户对存储空间的请求  。 每个容器都与针对数据和日志存储的某个 PVC 相关联。 在 Azure Kubernetes Service (AKS) 中，可以[创建永久性卷声明](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)，以便基于存储类自动预配存储。


此外，群集还存储密码、证书、密钥和其他敏感信息等的[机密](https://kubernetes.io/docs/concepts/configuration/secret/)  。

## <a name="deploy-the-availability-group-in-kubernetes"></a>在 Kubernetes 中部署可用性组

若要在 Kubernetes 中部署可用性组：

1. 创建 Kubernetes 群集

   对于一个可用性组，需要为 SQL Server 创建至少三个节点，并为主节点创建一个节点。

1. 部署运算符

1. 配置存储

1. 部署 StatefulSet

   运算符侦听有关部署 StatefulSet 的说明。 它将在三个单独的节点上自动创建 SQL Server 实例，并使用外部群集管理器配置可用性组。

1. 创建数据库并将其附加到可用性组

有关详细步骤，请参阅[为 SQL Server 容器创建 Always On 可用性组](sql-server-ag-kubernetes.md)。

## <a name="sql-server-kubernetes-operator"></a>SQL Server Kubernetes 运算符

部署运算符后，它会注册自定义 SQL Server 资源。 使用运算符部署此资源。  每个资源都与某个 SQL Server 的实例相对应并包含特定属性，如 `sapassword` 和 `monitoring policy`。 运算符分析资源并部署 Kubernetes StatefulSet。

StatfulSet 包含：

* mssql-server 容器

* mssql-ha-supervisor 容器

运算符、HA 主管和 SQL Server 的代码封装在名为 `mcr.microsoft.com/mssql/ha` 的 Docker 映像中。 此映像包含以下二进制文件：

* `mssql-operator`

    此过程部署为单独的 Kubernetes 部署。 它将注册名为 `SqlServer` (sqlservers.mssql.microsoft.com) 的 [Kubernetes 自定义资源](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)。 然后，它会侦听在 Kubernetes 群集中创建或更新的此类资源。 对于每个此类事件，它都会为相应的实例（例如 StatefulSet 或 `mssql-server-k8s-init-sql` 作业）创建或更新 Kubernetes 资源。

* `mssql-server-k8s-health-agent`

    此 web 服务器提供 Kubernetes [运行情况探测](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)以确定 SQL Server 实例的运行状况。 通过调用 `sp_server_diagnostics` 并将结果与监视器策略进行比较来监视本地 SQL Server 实例的运行状况。

* `mssql-ha-supervisor`

   维护 ag 证书和终结点。 

* `mssql-server-k8s-ag-agent`
  
    此过程监视单个 SQL Server 实例上的 AG 副本的运行状况，并执行故障转移。

    它还维护引导符选择。

* `mssql-server-k8s-init-sql`
  
    此 Kubernetes [作业](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)将所需状态配置应用于 SQL Server 实例。 每次创建或更新 SqlServer 资源时，运算符都会创建作业。 它确保与自定义资源对应的目标 SQL Server 实例具有资源中所述的所需配置。

    例如，如果需要以下任何设置，它会完成这些设置：
  * 更新 SA 密码
  * 为代理创建 SQL 登录名
  * 创建 DBM 终结点

* `mssql-server-k8s-rotate-creds`
  
    此 Kubernetes 作业实现“轮换凭据”任务。 创建此作业以请求更新 SA 密码、代理 SQL 登录密码、DBM 证书等。SA 密码指定为作业参数。 其他几项自动生成。

* `mssql-server-k8s-failover`

   Kubernetes 作业，用于实现手动故障转移工作流。

### <a name="notes"></a>说明

无论 AG 配置如何，运算符都将始终部署 HA 主管。 如果 SqlServer 资源未列出任何 AG，运算符仍将部署此容器。

用于运算符映像的版本与用于 SQL Server 映像的版本相同。

## <a name="next-steps"></a>后续步骤

> [Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
