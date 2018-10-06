---
title: 什么是 SQL 大数据群集数据池？ | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3a75f47148ff59d58d0d0d1397ba445b064c028f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795897"
---
# <a name="what-is-a-sql-big-data-clusters-data-pool"></a>什么是 SQL 大数据群集数据池？

本文介绍的角色*SQL Server 数据池*preview SQL Server 2019 中的大数据群集。 以下部分介绍的体系结构和功能的 SQL 数据池。

## <a name="data-pool-architecture"></a>数据池体系结构

数据池包含一个或多个 SQL Server 数据池实例。 SQL 数据池实例提供持久的 SQL Server 存储群集。 数据池用于引入数据从 SQL 查询或 Spark 作业。 若要跨大型数据集提供更好的性能，池中的数据的数据分布到分片在成员 SQL 数据池实例。

## <a name="scale-out-data-marts"></a>向外缩放数据市场

数据池可让向外缩放数据市场，其中将来自多个源的外部数据引入到数据池的创建。 由于数据分布于数据池实例，对组织有序数据的并行查询都很高效。

![向外缩放数据市场](media/concept-data-pool/data-virtualization-improvements.png)

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下概述：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
