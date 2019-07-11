---
title: 什么是存储池？
titleSuffix: SQL Server big data clusters
description: 本文介绍在 SQL Server 2019 大数据群集的存储池。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4d1ed459aa44de3855153f4316b82ca77db60049
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729094"
---
# <a name="what-is-the-storage-pool-sql-server-big-data-clusters"></a>什么是存储池 （SQL Server 大数据群集）？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍的角色*SQL Server 存储池*SQL Server 2019 大数据群集 （预览版） 中。 以下部分介绍的体系结构和功能的 SQL 存储池。

## <a name="storage-pool-architecture"></a>存储池体系结构

存储池包含的节点包含 SQL server on Linux、 Spark 和 HDFS 的存储。 SQL 大数据群集中的所有存储节点都是 HDFS 群集的成员。

![存储池体系结构](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>职责

存储节点负责：

- 通过 Spark 的数据引入。
- HDFS （Parquet 格式） 中的数据存储。 HDFS 还提供了数据持久性、 HDFS 数据分散存储在 SQL 大数据群集中的所有存储节点。
- 通过 HDFS 和 SQL Server 终结点的数据访问。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [研讨会：Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
