---
title: 什么是存储池？
titleSuffix: SQL Server big data clusters
description: 了解 SQL Server 存储池在 SQL Server 2019 大数据群集中的作用，以及 SQL 存储池的体系结构和功能。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fd7a38d555cbf6e2f64743f0907fbfbbdec4d41f
ms.sourcegitcommit: 6f49804b863fed44968ea5829e2c26edc5988468
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2020
ms.locfileid: "87806440"
---
# <a name="what-is-the-storage-pool-big-data-clusters-2019"></a>什么是存储池 ([!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)])？

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文介绍 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 中“SQL Server 存储池”的角色  。 以下部分介绍了 SQL 存储池的体系结构和功能。

## <a name="storage-pool-architecture"></a>存储池体系结构

存储池包含由 Linux 上的 SQL Server、Spark 和 HDFS 组成的存储节点。 SQL 大数据群集中的所有存储节点均为 HDFS 群集的成员。

![存储池体系结构](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>职责

存储节点负责：

- 通过 Spark 进行数据引入。
- HDFS 中的数据存储（Parquet 和带分隔符的文本格式）。 HDFS 还提供数据持久性，因为 HDFS 数据分散到 SQL 大数据群集中的所有存储节点上。
- 通过 HDFS 和 SQL Server 终结点进行数据访问。

## <a name="next-steps"></a>后续步骤

若要了解有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的详细信息，请参阅以下资源：

- [什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [Workshop:Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
