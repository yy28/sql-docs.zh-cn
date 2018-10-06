---
title: 什么是 SQL 大数据群集计算池？ | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: c17f6ac604edc021299f473137dcf6c5e470e3d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795983"
---
# <a name="what-is-a-sql-big-data-clusters-compute-pool"></a>什么是 SQL 大数据群集计算池？

本文介绍的角色*SQL Server 计算池*preview SQL Server 2019 中的大数据群集。 计算池提供大数据群集的横向扩展计算资源。 以下部分介绍的体系结构和计算池的功能。

## <a name="compute-pool-architecture"></a>计算池体系结构

计算池进行的其中一个或多个计算在 Kubernetes 中运行的 pod。 由协调的自动的创建和管理这些 pod [SQL Server 主实例](concept-master-instance.md)。 每个 pod 包含一组基本的服务和 SQL Server 数据库引擎的实例。

> [!NOTE]
> CTP 2.0 仅支持每个群集的单个计算池。

## <a name="scale-out-groups"></a>横向扩展组

计算池可以通过不同的数据源-如 HDFS、 Oracle、 MongoDB 或 Terradata 充当分布式查询的 PolyBase 横向扩展组。 通过使用在 Kubernetes 中的计算 pod，大数据群集可以自动执行创建和配置 PolyBase 横向扩展组的计算 pod。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下概述：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
