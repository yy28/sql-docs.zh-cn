---
title: 什么是大数据群集？
titleSuffix: SQL Server big data clusters
description: 了解在 Kubernetes 上运行的 SQL Server 2019 大数据群集 (预览版), 并提供用于关系数据和 HDFS 数据的向外缩放选项。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0beb4ea57ba6c2591e5b2c06a7775fc2d7e8b26c
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419496"
---
# <a name="what-are-sql-server-big-data-clusters"></a>什么是 SQL Server 大数据群集？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

从开始[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], SQL Server 大数据群集可让你部署在 Kubernetes 上运行的 SQL Server、Spark 和 HDFS 容器的可缩放群集。 这些组件是并行运行的, 使你能够从 Transact-sql 或 Spark 读取、写入和处理大数据, 从而使你可以轻松地将高价值的关系数据与大容量大数据组合在一起。

有关最新版本的新功能和已知问题的详细信息, 请参阅[发行说明](release-notes-big-data-cluster.md)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>方案

SQL Server 大数据群集可让你灵活地处理大数据。 您可以查询外部数据源, 通过 SQL Server 管理 HDFS 中的大数据, 或通过群集查询来自多个外部数据源的数据。 然后, 可以将数据用于 AI、机器学习和其他分析任务。 以下各节提供了有关这些方案的详细信息。

### <a name="data-virtualization"></a>数据虚拟化

通过利用[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), SQL Server 大数据群集可以在不移动或复制数据的情况下查询外部数据源。 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]引入数据源的新连接器。

![数据虚拟化](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data lake

SQL Server 大数据群集包含可缩放的 HDFS*存储池*。 这可用于存储大数据, 这可能会从多个外部源引入。 在大数据群集中将大数据存储在 HDFS 中后, 就可以分析和查询数据, 并将其与关系数据进行合并。

![Data lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>横向扩展数据市场

SQL Server 大数据群集提供了向外扩展计算和存储, 以提高分析任何数据的性能。 来自各种来源的数据可引入并分布在*数据池*节点上, 以便进行进一步分析。

![数据市场](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>集成 AI 和机器学习

SQL Server 大数据群集可对 HDFS 存储池中存储的数据和数据池启用 AI 和机器学习任务。 你可以使用 Spark 以及内置的 AI 工具在 SQL Server 中使用 R、Python、Scala 或 Java。

![AI 和 ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>管理和监视

通过结合使用命令行工具、Api、门户和动态管理视图来提供管理和监视。

你可以使用 Azure Data Studio 在大数据群集上执行各种任务。 这是通过新的**SQL Server 2019 扩展 (预览版)** 启用的。 此扩展提供:

- 用于常见管理任务的内置代码段。
- 能够浏览 HDFS、上传文件、预览文件和创建目录。
- 能够创建、打开和运行与 Jupyter 兼容的笔记本。
- 数据虚拟化向导, 用于简化外部数据源的创建。

## <a id="architecture"></a>种

SQL Server 大数据群集是由[Kubernetes](https://kubernetes.io/docs/concepts/)协调的 Linux 容器群集。

### <a name="kubernetes-concepts"></a>Kubernetes 概念

Kubernetes 是开源容器 orchestrator, 可根据需要缩放容器部署。 下表定义了一些重要的 Kubernetes 术语:

|||
|:--|:--|
| **Cluster** | Kubernetes 群集是一组称为节点的计算机。 一个节点控制群集并指定为主节点;其余节点是辅助角色节点。 Kubernetes 主机负责在辅助角色之间分配工作, 并负责监视群集的运行状况。 |
| **Node** | 节点运行容器化应用程序。 它可以是物理计算机, 也可以是虚拟机。 Kubernetes 群集可包含物理计算机和虚拟机节点的混合。 |
| **盒** | Pod 是 Kubernetes 的原子部署单元。 Pod 是运行应用程序所需的一个或多个容器和关联资源的逻辑组。 每个 pod 在节点上运行;节点可以运行一个或多个 pod。 Kubernetes master 会自动将 pod 分配给群集中的节点。 |
| &nbsp; ||

在 SQL Server 大数据群集中, Kubernetes 负责 SQL Server 大数据群集的状态;Kubernetes 构建和配置群集节点, 将 pod 分配给节点, 并监视群集的运行状况。

### <a name="big-data-clusters-architecture"></a>大数据群集体系结构

下图显示了 SQL Server 的大数据群集组件。

![体系结构概述](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a>控制器

控制器为群集提供管理和安全。 它包含 cntrol 服务、配置存储和其他群集级服务, 例如 Kibana、Grafana 和弹性搜索。

### <a id="computeplane"></a>计算池

计算池为群集提供计算资源。 它包含运行 Linux 上的 SQL Server pod 的节点。 计算池中的 pod 分为特定处理任务的*SQL 计算实例*。 

### <a id="dataplane"></a>数据池

数据池用于数据暂留和缓存。 数据池包括一个或多个运行 Linux 上的 SQL Server 的 pod。 它用于引入来自 SQL 查询或 Spark 作业的数据。 SQL Server 大数据群集数据市场将保留在数据池中。 

### <a name="storage-pool"></a>存储池

存储池包含由 Linux 上的 SQL Server、Spark 和 HDFS 组成的存储池。 SQL Server 大数据群集中的所有存储节点均为 HDFS 群集的成员。

> [!TIP]
> 若要深入了解大数据群集体系结构和安装, 请参阅[研讨会:Microsoft SQL Server 大数据群集体系](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)结构。

## <a name="next-steps"></a>后续步骤

SQL Server 大数据群集首先可以通过 SQL Server 2019 早期采用计划作为有限的公共预览。 若要请求访问, 请[在此处](https://aka.ms/eapsignup)注册, 并指定你对尝试大数据群集感兴趣。 Microsoft 将对所有请求进行会审, 并尽快做出响应。
