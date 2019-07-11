---
title: 数据池有哪些？
titleSuffix: SQL Server big data clusters
description: 本指南介绍了 SQL Server 2019 大数据群集中的数据池。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7530036cae939f6fd5d45fb5575f2161a36f21a1
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729124"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>在 SQL Server 大数据群集中的数据池有哪些？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍的角色*SQL Server 数据池*SQL Server 2019 大数据群集 （预览版） 中。 以下部分介绍的体系结构和功能的 SQL 数据池。

## <a name="data-pool-architecture"></a>数据池体系结构

数据池包含一个或多个 SQL Server 数据池实例。 SQL 数据池实例提供持久的 SQL Server 存储群集。 数据池用于引入数据从 SQL 查询或 Spark 作业。 若要跨大型数据集提供更好的性能，池中的数据的数据分布到分片在成员 SQL 数据池实例。

## <a name="scale-out-data-marts"></a>向外缩放数据市场

数据池可让向外缩放数据市场，其中将来自多个源的外部数据引入到数据池的创建。 由于数据分布于数据池实例，对组织有序数据的并行查询都很高效。

![向外缩放数据市场](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [研讨会：Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
