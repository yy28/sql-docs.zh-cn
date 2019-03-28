---
title: Always On 可用性组运行 Linux 的容器
titleSuffix: SQL Server
description: 本文介绍了 SQL Server 容器上的可用性组
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4b3d01538df675149a3cc7f555774c8d27bf4e14
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511064"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Always On 可用性组的 SQL Server 容器

SQL Server 2019 支持可用性组上的 Kubernetes 群集中的容器。 对于可用性组，部署 SQL Server [Kubernetes 运算符](https://coreos.com/blog/introducing-operators.html)到 Kubernetes 群集。 运算符可帮助包、 部署和管理可用性组在群集中。

![Kubernetes 容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上图中，四个节点 kubernetes 群集承载可用性组具有三个副本。 该解决方案包含以下组件：

* Kubernetes [*部署*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)。 部署包括运算符和配置映射。 这些提供容器映像、 软件和部署可用性组的 SQL Server 实例所需的说明。

* 三个节点，每个托管[ *StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)。 包含 StatefulSet [ *pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)。 包含每个 pod:
  * 运行一个 SQL Server 实例的 SQL Server 容器。
  * 可用性组代理。 

* 两个[ *ConfigMaps* ](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)与可用性组相关。 ConfigMaps 提供有关以下信息：
  * 运算符的部署。
  * 可用性组。

 * [*永久性卷*](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)是存储的片段。 一个*永久性卷声明*(PVC) 是由用户存储的请求。 每个容器隶属于数据和日志存储有关 PVC。 在 Azure Kubernetes 服务 (AKS) 中，你[创建永久性卷声明](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)到基于存储类自动预配存储。


此外，群集存储[*机密*](https://kubernetes.io/docs/concepts/configuration/secret/)密码、 证书、 密钥和其他敏感信息。

## <a name="deploy-the-availability-group-in-kubernetes"></a>部署在 Kubernetes 中的可用性组

若要部署 Kubernetes 中的可用性组：

1. 创建 Kubernetes 群集

   为可用性组，至少三个节点为创建 SQL Server 加上一个节点的母版。

1. 部署运算符

1. 配置存储

1. 部署 StatefulSet

   运算符侦听的说明部署 StatefulSet。 会自动在三个单独节点上创建的 SQL Server 实例和与外部群集管理器配置可用性组。

1. 创建数据库并将它们附加到可用性组

有关详细步骤，请参阅[Always On 可用性组的 SQL Server 容器](sql-server-ag-kubernetes.md)。

## <a name="sql-server-kubernetes-operator"></a>SQL Server Kubernetes 运算符

在部署该运算符后，它将注册自定义 SQL Server 资源。 使用运算符将部署此资源。  每个资源对应的 SQL Server 实例，包含特定属性，如`sapassword`和`monitoring policy`。 运算符将分析资源和部署 Kubernetes StatefulSet。

StatfulSet 包含：

* mssql-server container

* mssql-ha-supervisor container

运算符、 HA 监督程序和 SQL Server 的代码封装在名为的 Docker 映像`mcr.microsoft.com/mssql/ha`。 此映像包含以下二进制文件：

* `mssql-operator`

    此过程部署为单独的 Kubernetes 部署。 它会注册[Kubernetes 自定义资源](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)调用`SqlServer`(sqlservers.mssql.microsoft.com)。 然后它侦听此类资源正在创建或更新的 Kubernetes 群集中。 对于每个此类事件，它将创建或更新对应的实例的 Kubernetes 资源 (例如 StatefulSet 或`mssql-server-k8s-init-sql`作业)。

* `mssql-server-k8s-health-agent`

    此 web 服务器服务 Kubernetes[实时性探测](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)确定 SQL Server 实例的运行状况。 通过调用监视本地 SQL Server 实例的运行状况`sp_server_diagnostics`并将结果与监视器策略进行比较。

* `mssql-ha-supervisor`

   维护 ag 证书和终结点。 

* `mssql-server-k8s-ag-agent`
  
    此过程监视单个 SQL Server 实例上的可用性组副本的运行状况，并执行故障转移。

    它还维护群首选举。

* `mssql-server-k8s-init-sql`
  
    此 Kubernetes[作业](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)适用于 SQL Server 实例的所需的状态配置。 每次创建或更新 SqlServer 资源时，将运算符创建作业。 它可确保与自定义资源对应的目标 SQL Server 实例具有所需的资源中所述的配置。

    例如，如果任何以下设置是必需的它完成它们：
  * 更新的 SA 密码
  * 为代理创建 SQL 登录名
  * 创建了 DBM 端点

* `mssql-server-k8s-rotate-creds`
  
    此 Kubernetes 作业实现轮换凭据任务。 创建此作业，以请求更新的 SA 密码、 代理 SQL 登录密码、 DBM 证书等。SA 密码指定为作业参数。 其他类型是自动生成。

* `mssql-server-k8s-failover`

   Kubernetes 作业实现手动故障转移工作流。

### <a name="notes"></a>说明

而不考虑可用性组配置中，运算符始终将部署 HA 监督程序。 如果 SqlServer 资源不会列出任何可用性组，该运算符将仍部署此容器。

运算符映像的版本与 SQL Server 映像的版本相同。

## <a name="next-steps"></a>后续步骤

> [在 Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)
