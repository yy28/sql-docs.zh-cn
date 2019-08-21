---
title: 什么是数据池？
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 2019 大数据群集中的数据池。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bfd4d9d6ca24599a2297799555f53a83c6601420
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652268"
---
# <a name="what-are-data-pools-in-a-sql-server-big-data-cluster"></a>什么是 SQL Server 大数据群集中的数据池？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍了中[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] *SQL Server 数据池*的角色。 以下部分介绍了 SQL 数据池的体系结构和功能。

## <a name="data-pool-architecture"></a>数据池体系结构

数据池包含一个或多个 SQL Server 数据池实例。 SQL 数据池实例为群集提供持久的 SQL Server 存储。 数据池用于引入来自 SQL 查询或 Spark 作业的数据。 为了改善跨大型数据集的性能，数据池中的数据将分布到跨成员 SQL 数据池实例的分片中。

## <a name="scale-out-data-marts"></a>横向扩展数据市场

数据池支持创建横向扩展数据市场，其中将来自多个源的外部数据引入到数据池中。 由于数据分布在数据池实例上，因此对特选数据进行并行查询更有效。

![横向扩展数据市场](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>后续步骤

若要了解有关的[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]详细信息, 请参阅以下资源:

- [什么是[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [Workshop:Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
