---
title: "数据挖掘存储过程 (Analysis Services-数据挖掘) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: stored procedures [Analysis Services], data mining
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1d73a02535eb55e16de7058fa9f24dc335763f45
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="data-mining-stored-procedures-analysis-services---data-mining"></a>数据挖掘存储过程（Analysis Services - 数据挖掘）
  从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]开始， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持以任何托管语言编写的存储过程。 支持的托管语言包括 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET、C# 和托管 C++。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，可以使用 **CALL** 语句直接调用存储过程，或作为数据挖掘扩展插件 (DMX) 查询的一部分来调用。  
  
 有关调用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 存储过程的详细信息，请参阅 [调用存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)。  
  
 有关可编程性的常规信息，请参阅[数据挖掘编程](../../analysis-services/data-mining-programming.md)。  
  
 有关如何对数据挖掘对象编程的其他信息，请参阅 MSDN Library 中的文章“[SQL Server Data Mining Programmability](http://go.microsoft.com/fwlink/?LinkId=93735)（SQL Server 数据挖掘可编程性）”。  
  
> [!NOTE]  
>  查询挖掘模型时，特别是测试新的数据挖掘解决方案时，您可能会发现调用数据挖掘引擎内部使用的系统存储过程会很方便。 可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 查看这些系统存储过程的名称，以创建对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器的跟踪，然后创建、浏览和查询数据挖掘模型。 但是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不保证各个版本之间的系统存储过程的兼容性，您一定不要在生产系统中使用对系统存储过程的调用。 为了兼容性，您应使用 DMX 或 XML/A 创建自己的查询。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [SystemGetCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## <a name="see-also"></a>另请参阅  
 [交叉验证（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [交叉验证选项卡 &#40;挖掘准确性图表视图 &#41;](http://msdn.microsoft.com/library/bd215a68-1ad7-4046-9c44-ec8e2be13a64)   
 [调用存储过程](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  
