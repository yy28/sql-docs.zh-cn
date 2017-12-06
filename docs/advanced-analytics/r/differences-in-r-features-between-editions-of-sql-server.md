---
title: "在计算机学习功能的 SQL Server 的版本之间的差异 |Microsoft 文档"
ms.custom: 
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e599ab78d2b6a6ede13b1da1e6edf5167405fc2c
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>在计算机学习功能的 SQL Server 的版本之间的差异
 
 在 SQL Server 2016 和 SQL Server 2017 中提供了对机器学习的支持。 本文列出了支持功能的版本、 介绍适用于特定版本的其他限制并列出功能仅在某些版本中可用。

 > [!NOTE]
 > 一般情况下，SQL Server 机器学习不包括[操作化](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)Microsoft R Server 或机器学习服务器中包括的功能。
 > 
 > 如果你需要这些功能，你可以安装 Microsoft R Server 机学习单独，以支持的预测模型作为 web 服务的部署。 

## <a name="summary-of-differences"></a>差异摘要

-   **Enterprise Edition**
    
     SQL Server 2017 包括机器学习服务 （数据库中。 SQL Server 2016 包括 R Services。 此功能支持在 SQL Server，包括作为计算上下文使用 SQL Server 数据库中分析。
     
     SQL Server 2017 包括 Microsoft 机器学习 Server （独立）。 SQL Server 2016 包括 Microsoft R Server （独立）。 此功能支持机器学习不需要使用 SQL Server 作为计算上下文操作的化的。

     没有有关这些功能在 Enterprise Edition 中，可提供优化的性能和通过并行化和流式处理的可伸缩性限制。 此版本还可用于的平台支持流式处理和并行执行最大化。 这意味着，与不同的是 Standard Edition 中，输入数据不需要无法放入内存，但可以进行流式处理。
     
     使用 SQL Server 数据库中分析支持资源调控的外部脚本，以自定义服务器资源使用情况。
     
     较新版本的 Microsoft R Server 和机器学习服务器包括支持快速、 更安全的部署的操作化引擎改进的版本和共享的 R 解决方案。 有关详细信息，请参阅[具有可操作性分析使用机器学习服务器](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)。

-   **Developer Edition**

     功能与 Enterprise Edition 相同；但是，无法在生产环境中使用 Developer Edition。  
  
-   **Standard Edition**

     数据库中分析的所有功能已使用企业版，都包括资源调控除外。 性能和缩放也会受到限制： 可处理的数据必须能够容纳在服务器内存中，处理限制为单个计算线程，即使是在使用**RevoScaleR**函数。
  
-   **Express 和 Web 版本**
  
     仅 Express Edition with Advanced Services 包括机器学习功能。 性能限制与 Standard Edition 类似。 
     
     Web Edition 不用于任务，如创建机器学习模型。 但是，可以使用预测函数来执行评分在其他位置使用训练的模型。

-   **Azure SQL 数据库**
  
     初始测试在版本之后，R Services 目前**不**可用 Azure SQL 数据库中挂起的进一步开发。 

### <a name="external-script-languages-supported"></a>支持的外部脚本语言

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

开发人员版提供等效于的 Enterprise Edition 的性能。

用于生产环境不支持使用开发人员版。

## <a name="machine-learning-in-standard-edition"></a>Standard Edition 中的机器学习

在硬件配置相同的前提下，与标准 R 包相比，即使是 Standard Edition 也能提供一定的性能优势。

Standard Edition 不支持资源调控器。 有限的性能和可伸缩性与企业版和开发人员版相比，还提供了 standard Edition。

所有**RevoScaleR**函数和包使用标准版，包含在内，但它可以使用的进程数有限的服务的启动和管理 R 脚本。 此外，脚本处理的数据必须能够装入内存。

限制同样适用于使用的解决方案**revoscalepy**。

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>Express Edition with Advanced Services 中的机器学习

Express Edition 的限制与 Standard Edition 相同。

## <a name="machine-learning-in-web-edition"></a>Web Edition 中的机器学习

Web 版本不支持的 R 或 Python 脚本的执行。 但是，你可以使用[预测](../../t-sql/queries/predict-transact-sql.md)函数来执行[本机评分](../sql-native-scoring.md)已定型的不同的 SQL Server 或 R Server 实例和则保存在所需的二进制格式的模型上。

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅：

+ [SQL Server 2016 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [自 2017 年 SQL Server 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2017.md)

有关 SQL Server 中的其他功能的详细信息，请参阅：

+ [版本和 SQL Server 2016 支持的功能](../../sql-server/editions-and-components-of-sql-server-2016.md) 

有关如何可以优化解决方案中为大型数据集的详细信息，请参阅[对计算在 R 使用大数据的提示](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)文档。
