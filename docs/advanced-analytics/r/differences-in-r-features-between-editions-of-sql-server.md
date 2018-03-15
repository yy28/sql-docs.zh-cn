---
title: "SQL Server 计算机学习 Services 的版本之间的功能可用性 |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 16ca6c44b15c9fb7c1983d5a04175ebbade57895
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>跨版本的 SQL Server 计算机学习 Services 功能可用性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 机器学习功能均可在 SQL Server 2016 和 SQL Server 自 2017 年。 本文列出提供功能的版本、 介绍适用于特定版本的限制和列表仅在某些版本中可用的功能。

 > [!NOTE]
 > 一般情况下，SQL Server 机器学习 （数据库中） 不包括[操作化](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)独立 R 服务器或计算机学习服务器安装中包括的功能。 操作化包括 web 服务部署和托管应用程序，并因此争夺与其他 SQL Server 操作相同的资源。
 > 
 > 为此，我们建议在不同的物理服务器以支持的预测模型作为 web 服务的部署上安装 SQL Server 2016 R Server （独立） 或 SQL Server 自 2017 年 1 机器学习服务器 （独立）。 

## <a name="sql-server-2017-machine-learning-services-in-database-and-standalone"></a>SQL Server 自 2017 年 1 机器学习服务 （数据库） 和 （独立）

开发人员版提供等效于的 Enterprise Edition 的性能。 用于生产环境不支持使用开发人员版。

|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------|----------|--------|---|------------------------------|-------|
| R 解释程序 （&) 专有包 | 是 | 用户帐户控制 | 是 | “否” | 否 | 
| Python 解释器和客户端库 | 是 | 用户帐户控制 | 是 | “否” | 否 | 
| 分块的数据 <br/>（处理大量数据，超出什么所能容纳的内存） | 是 | 是 | “否” | “否” | 否 |
| 向上缩放处理 <br/>（2 个以上处理器） | 是 | 是 | “否” | “否” | 否 |
| 操作化 | 是 | 是 | “否” | “否” | 否 |
| [预测](../../t-sql/queries/predict-transact-sql.md)函数 <br/>(执行[本机评分](../sql-native-scoring.md)预先训练的模型，之前保存在所需的二进制格式中) | 是 | 用户帐户控制 | 用户帐户控制 | 用户帐户控制 | 是 |
| R 客户端兼容性 | 是 | 用户帐户控制 | 是 | “否” | 否 | 
| Microsoft R Open | 是 | 用户帐户控制 | 是 | “否” | 否 | 
| Anaconda Python 3.5 | 是 | 用户帐户控制 | 是 | “否” | 否 | 

## <a name="sql-server-2016-r-services-in-database-and-r-server-standalone"></a>SQL Server 2016 R Services （数据库） 和 R Server （独立）

自 2017 年 1，这不是第一次 2016年发行版的一部分的 Python 支持减相同功能的可用性。

## <a name="r-feature-availability-in-azure-sql-database"></a>Azure SQL 数据库中的 R 功能可用性
  
初始测试在版本之后，R Services 目前**不**可用 Azure SQL 数据库中挂起的进一步开发。 

## <a name="performance-expectations-for-enterprise-edition"></a>对性能的预期要求 Enterprise Edition

中的计算机学习解决方案的性能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]预计通常超过使用传统 R，给定的相同硬件的实现。 是因为 SQL Server 中 R 解决方案可以运行使用服务器资源和有时分发到多个进程使用**RevoScaleR**函数。 

性能具有不已评估 Python 解决方案的功能是仍处于开发阶段，但是部分相同的优点所需应用。

用户还可能会看到在性能和相同的机器学习解决方案，如果在 Enterprise Edition vs 中运行的可伸缩性的很大差异。很大的差异。 原因包括支持并行处理，可用于机器学习，增加的线程和流式处理 （或分块），这样 RevoScaleR 函数来处理数据超过了内存中可以容纳该值。 

但是，即使在相同的硬件上的性能可以通过在 R 或 Python 代码的外部的许多因素影响。 这些因素包括对服务器资源的竞争需求、 创建的查询计划的类型、 架构更改，需要更新统计信息或创建新的查询计划、 碎片，和的详细信息。 可以存储的过程包含 R 或 Python 代码可能会以秒为单位在一个工作负荷下运行，但需要分钟时有运行的其他服务。  因此，我们建议你监视服务器性能，包括网络，对于远程计算上下文，在衡量机学习性能的多个方面。

我们还建议你配置[资源调控器](../../relational-databases/resource-governor/resource-governor.md)（Enterprise Edition 中推出） 自定义外部脚本作业是按优先级排列，或处理大量服务器工作负载下的方式。 你可以定义分类器函数来指定外部脚本作业的源和按优先级排列某些工作负荷、 限制 SQL 查询使用的内存量和控制并行工作负荷基础上使用的进程数。

## <a name="see-also"></a>另请参阅

+ [SQL Server 2016 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [自 2017 年 SQL Server 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [对计算在 R （机器学习服务器） 使用大数据的提示](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
