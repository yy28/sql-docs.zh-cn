---
title: 什么是 SQL Server 大数据群集存储池？ | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 100ce09f7066a6df33d7b1daaf50db50bda4ed03
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795904"
---
# <a name="what-is-the-sql-server-big-data-clusters-storage-pool"></a>什么是 SQL Server 大数据群集存储池？

本文介绍的角色*SQL Server 存储池*preview SQL Server 2019 中的大数据群集。 以下部分介绍的体系结构和功能的 SQL 存储池。

## <a name="storage-pool-architecture"></a>存储池体系结构

存储池包含的节点包含 SQL server on Linux、 Spark 和 HDFS 的存储。 SQL 大数据群集中的所有存储节点都是 HDFS 群集的成员。

![存储池体系结构](media/concept-storage-pool/scale-big-data-on-demand.png)

## <a name="responsibilities"></a>职责

存储节点负责：

- 通过 Spark 的数据引入。
- HDFS （Parquet 格式） 中的数据存储。 HDFS 还提供了数据持久性、 HDFS 数据分散存储在 SQL 大数据群集中的所有存储节点。
- 通过 HDFS 和 SQL Server 终结点的数据访问。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下概述：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
