---
title: 什么是 SQL Server 2019 大数据群集？ | Microsoft Docs
description: 了解有关 SQL Server 2019 大数据群集 （预览版），在 Kubernetes 上运行并提供 HDFS 数据以及关系的向外缩放选项。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/25/2018
ms.topic: overview
ms.prod: sql
ms.openlocfilehash: 603e84f3f4e1e27052df6996ae06933ace585c0f
ms.sourcegitcommit: 3a8293b769b76c5e46efcb1b688bffe126d591b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226279"
---
# <a name="what-are-sql-server-2019-big-data-clusters"></a>什么是 SQL Server 2019 大数据群集？

从开始[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]，SQL Server 大数据群集允许你部署的 Kubernetes 上运行的 SQL Server、 Spark 和 HDFS 容器的可缩放群集。 并行运行这些组件，以使您能够读取、 写入，并处理从 TRANSACT-SQL 或 Spark 的大数据、 使您轻松合并和分析大数据大容量高价值关系数据。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>方案

SQL Server 大数据群集提供在如何与你的大数据进行交互的灵活性。 您可以查询外部数据源，将大数据存储在 HDFS 由 SQL Server 或通过群集的多个外部数据源查询数据。 然后，您可以使用数据的 AI、 机器学习和其他分析任务。 以下部分提供有关这些方案的详细信息。

### <a name="data-virtualization"></a>数据虚拟化

通过利用[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md)，SQL Server 大数据群集可以查询外部数据源，而无需移动或复制数据。 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 到数据源引入了新的连接器。

![数据虚拟化](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>数据湖

SQL Server 大数据群集包括可缩放的 HDFS*存储池*。 这可以用于存储来自多个外部源可能会引入的大数据。 一旦大数据群集中情况下，大数据存储在 HDFS 中，可以分析和查询数据并将其与关系数据。

![数据湖](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>向外缩放数据市场

SQL Server 大数据群集提供横向扩展计算和存储空间来提高分析任何数据的性能。 从各种源的数据可以引入和分布*数据池*作为以做进一步分析缓存的节点。

![数据市场](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>集成的 AI 和机器学习

SQL Server 大数据群集启用 AI 和机器学习的数据存储在 HDFS 存储池和数据池上的任务。 可以使用 Spark，以及内置 AI 工具中使用 R、 Python、 Scala、 或 Java 的 SQL Server。

![AI 和机器学习](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>管理和监视

通过组合使用命令行工具、 Api、 管理员门户和动态管理视图提供了管理和监视。

[群集管理员门户](cluster-admin-portal.md)是群集中将显示状态和运行状况的 pod 的 web 界面。 它还提供用于日志分析和监视仪表板的链接到其他仪表板。

Azure Data Studio 可用于大数据群集上执行各种任务。 这新启用**SQL Server 2019 扩展 （预览版）**。 此扩展提供了：

- 有关常见管理任务的内置代码段。
- 浏览 HDFS，功能将文件上传、 预览文件，并创建目录。
- 能够创建、 打开，并运行兼容的 Jupyter 笔记本。
- 数据虚拟化向导来简化的外部数据源创建。

## <a id="architecture"></a> 体系结构

SQL Server 大数据群集是由协调的 Linux 容器的群集[Kubernetes](https://kubernetes.io/docs/concepts/)。

### <a name="kubernetes-concepts"></a>Kubernetes 概念

Kubernetes 是开放源代码容器业务流程协调程序，可以缩放容器部署，根据需求。 下表定义了一些重要的 Kubernetes 术语：

|||
|--|--|
| **Cluster** | Kubernetes 群集是一组计算机，称为节点。 一个节点控制群集，并指定主节点;剩余的节点是辅助角色节点。 Kubernetes 主机是负责分发在辅助角色之间的工作，并监视群集的运行状况。 |
| **Node** | 节点运行容器化应用程序。 它可以是物理机或虚拟机。 Kubernetes 群集可以包含的物理机和虚拟机节点的组合。 |
| **Pod** | Pod 是 Kubernetes 的原子部署单位。 Pod 是一个或多个容器的逻辑组 — 和关联的资源，需要运行应用程序。 每个 pod 的节点; 上运行节点可以运行一个或多个 pod。 Kubernetes 主机会自动分配到群集中节点的 pod。 |

在 SQL Server 大数据群集中，Kubernetes 负责 SQL Server 大数据群集; 的状态Kubernetes 构建和配置群集节点，将 pod 分配给节点，并监视群集的运行状况。

### <a name="big-data-clusters-architecture"></a>大数据群集体系结构

在群集中的节点分为三个逻辑平面： 控制平面、 计算窗格和数据平面。 每个平面群集中具有不同的职责。 在 SQL Server 大数据群集中的每个 Kubernetes 节点托管组件的至少一个平面的 pod。

![体系结构概述](media/big-data-cluster-overview/architecture-diagram-planes.png)

### <a id="controlplane"></a> 控制平面

控制平面提供管理和安全的群集。 它包含 Kubernetes 主机*SQL Server 主实例*，和其他群集级别服务，例如 Hive 元存储和 Spark 驱动程序。

### <a id="computeplane"></a> 计算平面

计算平面提供到群集的计算资源。 它包含在 Linux pod 上运行 SQL Server 的节点。 计算平面中的 pod 分为*计算池*特定处理任务。 计算池可以充当[PolyBase](../relational-databases/polybase/polybase-guide.md)横向扩展组中通过不同的数据源的分布式查询 — 例如 HDFS、 Oracle、 MongoDB 或 Teradata。

### <a id="dataplane"></a> 数据平面

数据平面用于数据暂留和缓存。 它包含的 SQL 数据池和存储池。  SQL 数据池包含在 Linux 上运行 SQL Server 的一个或多个 pod。 它用于从 SQL 查询或 Spark 作业引入数据。 SQL Server 大数据群集的数据集市将保留在数据池。 存储池包含的存储池 pod 组成 Linux、 Spark 和 HDFS 上的 SQL Server。 在 SQL Server 大数据群集中的所有存储节点都是 HDFS 群集的成员。

## <a name="next-steps"></a>后续步骤

SQL Server 大数据群集将为通过 SQL Server 2019 早期采用计划的有限公共预览版发布。 若要请求访问权限，注册[此处](https://aka.ms/eapsignup)，并指定尝试大数据群集的关注。 Microsoft 将会审的所有请求，并尽可能快地做出响应。
