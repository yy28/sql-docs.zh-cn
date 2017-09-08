---
title: "在计算机学习功能的 SQL Server 的版本之间的差异 |Microsoft 文档"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9b520b7fc7e97498f4b46a43ad991558025123a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---

# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>在计算机学习功能的 SQL Server 的版本之间的差异
 
 对机器学习支持以下版本的 SQL Server 2016 和 SQL Server 2017 有：

## <a name="summary-of-differences"></a>差异摘要

-   **Enterprise Edition**
    
     SQL Server 2017 包括机器学习服务 （数据库中。 SQL Server 2016 包括 R Services。 此功能支持在 SQL Server，包括作为计算上下文使用 SQL Server 数据库中分析。
     
     SQL Server 2017 包括 Microsoft 机器学习 Server （独立）。 SQL Server 2016 包括 Microsoft R Server （独立）。 此功能支持机器学习不需要使用 SQL Server 作为计算上下文操作的化的。

     没有有关这些功能在 Enterprise Edition 中，可提供优化的性能和通过并行化和流式处理的可伸缩性限制。 此版本还可用于的平台支持流式处理和并行执行最大化。
     
     使用 SQL Server 数据库中分析支持资源调控的外部脚本，以自定义服务器资源使用情况。
     
     较新版本的 Microsoft R Server 包括改进的版本支持快速、 更安全的部署的操作化引擎和共享的 R 解决方案。 有关详细信息，请参阅[mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)。

-   **Developer Edition**

     功能与 Enterprise Edition 相同；但是，无法在生产环境中使用 Developer Edition。  
  
-   **Standard Edition**

     数据库中分析的所有功能已使用企业版，都包括资源调控除外。 性能和可扩展性还会受到限制： 可处理的数据必须能够容纳在服务器内存中，处理限制为单个计算线程，即使是在使用**RevoScaleR**函数。
  
-   **Express 和 Web 版本**
  
     仅 Express Edition with Advanced Services 包括机器学习功能。 性能限制与 Standard Edition 类似。 Web edition 不用于任务，如创建机器学习模型;但是，可以使用预测函数来执行评分在其他位置使用训练的模型。

-   **Azure SQL 数据库**
  
     Azure SQL 数据库中当前不支持机器学习功能，如 R 和 Python 脚本。
     
     有关详细信息，以及有关此功能何时可用，公告，请参阅 SQL Server 博客： [Python 中 SQL Server 2017： 增强数据库中机器学习](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


### <a name="languages-supported-in-all-editions"></a>在所有版本中受支持的语言

对于所有版本支持以下机器学习语言：

+ SQL Server 2017: R 和 Python
+ 仅 SQL Server 2016: R

所有版本都随附 Microsoft R Open。

Microsoft R Client 适用于所有版本。

## <a name="machine-learning-in-enterprise-edition"></a>Enterprise Edition 中的机器学习

中的计算机学习解决方案的性能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]预计通常超过使用传统 R，给定的相同硬件的实现。 是因为 SQL Server 中 R 解决方案可以运行使用服务器资源和有时分发到多个进程使用**RevoScaleR**函数。 

性能具有不已评估 Python 解决方案的功能是仍处于开发阶段，但是部分相同的优点所需应用。

用户还可能会看到在性能和相同的机器学习解决方案，如果在 Enterprise Edition vs 中运行的可伸缩性的很大差异。很大的差异。 原因包括支持并行处理，可用于机器学习，增加的线程和流式处理 （或分块），这样 RevoScaleR 函数来处理数据超过了内存中可以容纳该值。 

但是，即使在相同的硬件上的性能可以通过在 R 或 Python 代码的外部的许多因素影响。 这些因素包括对服务器资源的竞争需求、 创建的查询计划的类型、 架构更改，需要更新统计信息或创建新的查询计划、 碎片，和的详细信息。 可以存储的过程包含 R 或 Python 代码可能会以秒为单位在一个工作负荷下运行，但需要分钟时有运行的其他服务。  因此，我们建议你监视服务器性能，包括网络，对于远程计算上下文，在衡量机学习性能的多个方面。

我们还建议你配置[资源调控器](../../relational-databases/resource-governor/resource-governor.md)（Enterprise Edition 中推出） 自定义外部脚本作业是按优先级排列，或处理大量服务器工作负载下的方式。 你可以定义分类器函数来指定外部脚本作业的源和按优先级排列某些工作负荷、 限制 SQL 查询使用的内存量和控制并行工作负荷基础上使用的进程数。

## <a name="machine-learning-in-developer-edition"></a>开发人员版中的机器学习

Developer Edition 提供的性能与 Enterprise Edition 相当；但是，不支持在生产环境中使用 Developer Edition。

## <a name="machine-learning-in-standard-edition"></a>Standard Edition 中的机器学习

在硬件配置相同的前提下，与标准 R 包相比，即使是 Standard Edition 也能提供一定的性能优势。

Standard Edition 不支持资源调控器。 使用资源调控是自定义服务器资源，以支持各种工作负荷，如模型定型集和评分的最佳方式。

此外，与 Enterprise Edition 和 Developer Edition 相比，Standard Edition 提供的性能和可伸缩性有限。 所有**RevoScaleR**函数和包使用标准版，包含在内，但它可以使用的进程数有限的服务的启动和管理 R 脚本。 此外，脚本处理的数据必须能够装入内存。  限制同样适用于使用的解决方案**revoscalepy**。

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>Express Edition with Advanced Services 中的机器学习

Express Edition 的限制与 Standard Edition 相同。

## <a name="machine-learning-in-web-edition"></a>Web Edition 中的机器学习

Web 版本不支持的 R 或 Python 脚本的执行。 但是，你可以使用预测函数执行[本机评分](../sql-native-scoring.md)已定型的不同的 SQL Server 或 R Server 实例和则保存在所需的二进制格式的模型上。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅：

+ [SQL Server 2016 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [自 2017 年 SQL Server 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2017.md)

有关 SQL Server 中的其他功能的详细信息，请参阅：

+ [SQL Server 2016 的各版本和支持的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 

有关 Microsoft R 功能和如何可以优化解决方案中为大型数据集的详细信息，请参阅[Microsoft R Server](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)文档。
