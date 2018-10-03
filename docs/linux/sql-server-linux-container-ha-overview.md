---
title: SQL Server 容器的高可用性
description: 本文介绍了 SQL Server 容器的高可用性
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: ccf4b3bab89c29fde1ff592a166baa3747afa890
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843217"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server 容器的高可用性

创建和管理 SQL Server 实例以本机方式在 Kubernetes 中。

将 SQL Server 部署到由管理的 docker 容器[Kubernetes](https://kubernetes.io/)。 在 Kubernetes 中，在群集节点发生故障的情况下，可以自动恢复与 SQL Server 实例的容器。 更可靠的可用性，配置 SQL Server Always On 可用性组上的 Kubernetes 群集的容器中的 SQL Server 实例。 本文比较了两个解决方案。

## <a name="compare-sql-server-versions-on-kubernetes"></a>在 Kubernetes 上的 SQL Server 版本比较

SQL Server 2017 提供在 Kubernetes 上部署的 Docker 映像。 可以使用 Kubernetes 永久性卷声明 (PVC) 来配置该映像。 Kubernetes 监视 SQL Server 进程在容器中。 如果进程、 pod、 容器或节点发生故障，Kubernetes 将自动启动另一个实例，并重新连接到存储。

SQL Server 2019 引入了与 Kubernetes StatefulSet 更可靠就。 这样，Kubernetes 安排在可以加入 SQL Server Always On 可用性组中的容器映像中的 SQL Server 实例。 这可以提供改进的运行状况监视，更快地恢复，卸载备份，并读出规模。  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>与在 Kubernetes 上的 SQL Server 实例的容器

Kubernetes 版本 1.6 和更高版本已支持[*存储类*](http://kubernetes.io/docs/concepts/storage/storage-classes/)， [*永久性卷声明*](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)，和[ *Azure 磁盘的卷类型*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)。 

在此配置中，Kubernetes 充当容器业务流程协调程序的角色。 

![Kubernetes SQL Server 群集的关系图](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

在上图中，`mssql-server`中是一个 SQL Server 实例 （容器） [ *pod*](http://kubernetes.io/docs/concepts/workloads/pods/pod/)。 一个[副本集](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)可确保在节点发生故障后自动恢复 pod。 应用程序连接到服务。 在这种情况下，该服务表示承载的发生故障后保持不变的 IP 地址的负载均衡器`mssql-server`。

Kubernetes 会协调群集中的资源。 当 pod 或托管在容器中的 SQL Server 实例的节点失败时，业务流程协调程序会引导 SQL Server 实例具有相同 pod 中的容器，并将其附加到相同的持久存储。

SQL Server 2017 和更高版本支持容器的 Kubernetes 上。

若要在 Kubernetes 中创建一个容器，请参阅[部署在 Kubernetes 中的 SQL Server 容器](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>SQL Server Always On 可用性组上在 Kubernetes 中的 SQL Server 容器

SQL Server 2019 在 Kubernetes 中的容器上支持可用性组。 对于可用性组，部署 SQL Server [Kubernetes 运算符](http://coreos.com/blog/introducing-operators.html)到 Kubernetes 群集。 运算符可帮助包、 部署和管理 SQL Server 实例和可用性组在群集中。

![Kubernetes 容器中的 AG](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

在上图中，四个节点 kubernetes 群集承载可用性组具有三个副本。 该解决方案包含以下组件：

* Kubernetes [*部署*](http://kubernetes.io/docs/concepts/workloads/controllers/deployment/)。 部署包括运算符和配置映射。 这些提供容器映像、 软件和部署可用性组的 SQL Server 实例所需的说明。

* 三个节点，每个托管[ *StatefulSet*](http://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)。 StatefulSet 包含一个 pod。 包含每个 pod:
  * 运行一个 SQL Server 实例的 SQL Server 容器。
  * 监督程序`mcr.microsoft.com/mssql/ha`用于管理可用性组。

* 两个[ *ConfigMaps* ](http://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)与可用性组相关。 ConfigMaps 提供有关以下信息：
  * 运算符的部署。
  * 可用性组。

 * 为每个 SQL Server 实例的永久性卷的数据和日志文件提供存储。

此外，群集存储[*机密*](http://kubernetes.io/docs/concepts/configuration/secret/)密码、 证书、 密钥和其他敏感信息。

## <a name="compare-sql-server-high-availabiltiy-on-containers-with-and-without-the-availability-group"></a>比较使用和不使用可用性组的容器上的 SQL Server 高可用性

以下表 compairs 容器的 Kubernetes 上使用和不可用性组中的 SQL Server 高可用性功能：

| |与某个可用性组 | 独立容器实例<br/> 无可用性组
|:------|:------|:------
|自动从节点故障中恢复 | 用户帐户控制 | 用户帐户控制
|自动从 pod 故障中恢复 | 用户帐户控制 | 用户帐户控制
|更快故障转移 |用户帐户控制 |
|自动从 SQL Server 实例故障中恢复 | 用户帐户控制 | 
|自动从数据库运行状况检查失败中恢复 | 用户帐户控制 | 
|提供只读副本 | 用户帐户控制 |
|辅助副本备份 | 用户帐户控制 | 
|StatefulSet 作为运行 | 用户帐户控制 | 

一个主要区别是通过在容器中的 SQL Server 的单个实例的可用性组相比更快地恢复 （或故障转移） 时间。 这是因为 SQL Server 可用性组在群集中其他节点上将可用性组数据库的次要副本。 故障转移时，辅助副本是选择并升级为主要副本。 连接到服务的应用程序将重定向到新的主副本。 

没有可用性组中，当 Kubernetes 检测到故障转移，它需要进行创建容器，将其连接到存储，，然后连接到服务的应用程序重新连接在一起。 确切的故障转移时间取决于其中已故障转移，以及如何检测到它。 

通常情况下，可用性组的故障转移时间以秒为单位，尽管要恢复容器的单个实例的故障转移时间可能最多 10 分钟。

## <a name="next-steps"></a>后续步骤

若要将 SQL Server 容器在 Azure Kubernetes 服务 (AKS) 部署，请遵循以下教程之一：

* [部署 Docker 容器中的 SQL Server](sql-server-linux-configure-docker.md)
* [将 SQL Server 容器在 Kubernetes 中部署](tutorial-sql-server-containers-kubernetes.md)
* [部署 SQL Server Always On 可用性组 Kubernetes](tutorial-sql-server-ag-kubernetes.md)

