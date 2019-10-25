---
title: 什么是计算池？
titleSuffix: SQL Server big data clusters
description: 本文介绍了 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]中的计算池。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 420c4705d86eb55b6b99a6cf432cb95f3b9a6694
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798243"
---
# <a name="what-are-compute-pools-in-a-sql-server-big-data-cluster"></a>什么是 SQL Server 大数据群集中的计算池？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍 SQL Server 2019 大数据群集（预览版）中 SQL Server 计算池的作用。 计算池为大数据群集提供横向扩展计算资源。 以下部分介绍计算池的体系结构和功能。

## <a name="compute-pool-architecture"></a>计算池体系结构

计算池由 Kubernetes 中运行的一个或多个计算 pod 组成。 由 [SQL Server 主实例](concept-master-instance.md)来协调这些 pod 的自动创建和管理过程。 每个 pod 包含一组基本服务和一个 SQL Server 数据库引擎的实例。

## <a name="scale-out-groups"></a>横向扩展组

计算池可充当针对不同数据源的分布式查询（例如 HDFS、Oracle、MongoDB 或 Teradata）的 PolyBase 横向扩展组。 通过使用 Kubernetes 中的计算 pod，大数据群集可以自动创建和配置 PolyBase 横向扩展组的计算 pod。

## <a name="next-steps"></a>后续步骤

若要了解有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的详细信息，请参阅以下资源：

- [什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [研讨会： Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
