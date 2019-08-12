---
title: 什么是存储池？
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 2019 大数据群集中的存储池。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 58e6f16a088d6dc6c1fc6bd32297e7bd698acbbf
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958650"
---
# <a name="what-is-the-storage-pool-sql-server-big-data-clusters"></a>什么是存储池（SQL Server 大数据群集）？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍 SQL Server 2019 大数据群集（预览版）中“SQL Server 存储据池”的角色  。 以下部分介绍了 SQL 存储池的体系结构和功能。

## <a name="storage-pool-architecture"></a>存储池体系结构

存储池包含由 Linux 上的 SQL Server、Spark 和 HDFS 组成的存储节点。 SQL 大数据群集中的所有存储节点均为 HDFS 群集的成员。

![存储池体系结构](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>责任

存储节点负责：

- 通过 Spark 进行数据引入。
- HDFS 中的数据存储（Parquet 格式）。 HDFS 还提供数据持久性，因为 HDFS 数据分散到 SQL 大数据群集中的所有存储节点上。
- 通过 HDFS 和 SQL Server 终结点进行数据访问。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [研讨会：Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
