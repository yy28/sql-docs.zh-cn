---
title: SQL Server 计算机学习 Services 的版本之间的功能可用性 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cdb3e54addb2137e7c0ae2d6462be9c75c542539
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="feature-availability-across-editions-of-sql-server-machine-learning-services"></a>跨版本的 SQL Server 计算机学习 Services 功能可用性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 机器学习功能均可在 SQL Server 2016 和 SQL Server 自 2017 年。 本文列出提供功能的版本、 介绍适用于特定版本的限制和列表仅在某些版本中可用的功能。


## <a name="sql-server-2017-features"></a>SQL Server 2017 功能

企业版和开发人员版具有相同的功能覆盖率，以便您可以而不会产生开销相同生成用于企业安装解决方案。 虽然各个版本在功能上等效，开发人员版的使用不是支持用于生产环境。

基本和高级集成之间的区别是小数位数。 高级的集成可用于在你的计算机可以容纳任何大小的数据集的并行处理所有可用的内核数。 仅限于 2 个核心以及到数据集在内存中不超过基本集成。 

基本和高级集成适用于 （数据库） 实例。 独立服务器不是数据库引擎实例功能，并作为安装选项仅在开发人员和企业版中提供。

|功能|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|基本 R 集成|是|用户帐户控制|用户帐户控制|用户帐户控制|否|   
|高级 R 集成|是|是|“否”|“否”|否| 
|基本 Python 集成|是|用户帐户控制|用户帐户控制|用户帐户控制|否|
|高级 Python 集成|是|是|“否”|“否”|否| 
|机器学习服务器（独立）|是|是|“否”|“否”|否|   

 > [!NOTE]
 > 仅 （独立） 服务器提供[操作化](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)Microsoft （非 SQL 品牌） R 服务器或计算机学习服务器安装中包括的功能。 操作化包括 web 服务部署和承载功能。
>
> 对于 （数据库中） 安装，来实现解决方案的等效方法利用数据库引擎的功能时将代码转换为可以运行存储过程中的函数。


## <a name="sql-server-2016-r-features"></a>SQL Server 2016 R 功能

SQL Server 2016 包括仅 R 集成。 在 SQL Server 2016，基本和高级 R 集成是等效于 SQL Server 自 2017 年。

## <a name="r-feature-availability-in-azure-sql-database"></a>Azure SQL 数据库中的 R 功能可用性
  
初始测试在版本之后，R Services 已从 Azure SQL 数据库，挂起的进一步开发。 

## <a name="performance-expectations-for-enterprise-edition"></a>对性能的预期要求 Enterprise Edition

中的计算机学习解决方案的性能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]预计通常超过使用传统 R，给定的相同硬件的实现。 是因为 SQL Server 中 R 解决方案可以运行使用服务器资源和有时分发到多个进程使用**RevoScaleR**函数。 

用户还可能会看到在性能和相同的机器学习解决方案，如果在 Enterprise Edition vs 中运行的可伸缩性的很大差异。很大的差异。 原因包括支持并行处理，可用于机器学习，增加的线程和流式处理 （或分块），这样 RevoScaleR 函数来处理数据超过了内存中可以容纳该值。 

但是，即使在相同的硬件上的性能可以通过在 R 或 Python 代码的外部的许多因素影响。 这些因素包括对服务器资源的竞争需求、 创建的查询计划的类型、 架构更改，需要更新统计信息或创建新的查询计划、 碎片，和的详细信息。 可以存储的过程包含 R 或 Python 代码可能会以秒为单位在一个工作负荷下运行，但需要分钟时有运行的其他服务。  因此，我们建议你监视服务器性能，包括网络，对于远程计算上下文，在衡量机学习性能的多个方面。

我们还建议你配置[资源调控器](../../relational-databases/resource-governor/resource-governor.md)（Enterprise Edition 中推出） 自定义外部脚本作业是按优先级排列，或处理大量服务器工作负载下的方式。 你可以定义分类器函数来指定外部脚本作业的源和按优先级排列某些工作负荷、 限制 SQL 查询使用的内存量和控制并行工作负荷基础上使用的进程数。

## <a name="see-also"></a>另请参阅

+ [SQL Server 2016 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [自 2017 年 SQL Server 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2017.md)
+ [对计算在 R （机器学习服务器） 使用大数据的提示](https://docs.microsoft.com/machine-learning-server/r/tutorial-large-data-tips)
