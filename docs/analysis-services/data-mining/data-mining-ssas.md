---
title: "数据挖掘 (SSAS) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 23048ed60a625a573d4820435f4ba87c0375e013
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-ssas"></a>数据挖掘 (SSAS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过提供 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的数据挖掘，是自 2000 版本以来预测分析方面的领导者。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘的组合提供了针对预测分析的集成平台，其中包含数据清理和准备、机器学习和报告。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘包括多个标准算法，包括 EM 和 K-Means 群集模型、神经网络、逻辑回归和线性回归、决策树和 naive bayes 分类器。 所有模型具有集成的可视化效果，以帮助开发、优化和评估模型。  将数据挖掘集成到商业智能解决方案可帮助你针对复杂问题做出明智决策。  
  
## <a name="benefits-of-data-mining"></a>数据挖掘的优点  
 数据挖掘（也称为预测分析和机器学习）使用精心研究的统计原则来发现数据中的模式。 通过将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的数据挖掘算法应用于您的数据，您可以预测趋势、标识模式、创建规则和建议、分析复杂数据集中的事件顺序以及洞察新情况。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的数据挖掘不仅功能强大和易于访问，并且与许多人在进行分析和报告工作时喜欢使用的工具集成在一起。  
  
## <a name="key-data-mining-features"></a>关键数据挖掘功能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘提供了以下支持集成数据挖掘解决方案的功能：  
  
-   多个数据源：对于数据挖掘，可使用任何表格形式的数据源，包括电子表格和文本文件。 此外，您还可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中轻松地挖掘创建的 OLAP 多维数据集。 但是，不能使用内存中数据库的数据。  
  
-   集成的数据清理、数据管理和报表： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了用于分析和清理数据的工具。 可构建 ETL 过程，用于清理数据以准备建模，ssISnoversion 也可使重新定型和更新模型更加容易。  
  
-   多个可自定义的算法：除了提供聚类分析、神经网络和决策树之类的算法之外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘还支持开发自定义的插件算法。  
  
-   模型测试基础结构：使用重要的统计工具（例如交叉验证、分类矩阵、提升图和散点图）测试您的模型和数据集。 轻松创建和管理测试和定型集。  
  
-   查询和钻取： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘提供 DMX 语言，用于将预测查询集成到应用程序中。 此外，还可以从模型中检索详细统计信息和模式，并钻取到事例数据。  
  
-   客户端工具：除了 SQL Server 提供的开发和设计工具之外，您还可以使用 Excel 数据挖掘外接程序来创建、查询和浏览模型。 或者，创建自定义的客户端，包括 Web 服务。  
  
-   脚本语言支持和托管 API：所有数据挖掘对象都是完全可编程的。 可通过用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的 MDX、XMLA 或 PowerShell 扩展插件来撰写脚本。 使用数据挖掘扩展插件 (DMX) 语言来进行快速查询和脚本撰写。  
  
-   安全性和部署：通过 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供基于角色的安全性，包括用于钻取到模型和结构数据的单独权限。 轻松地将模型部署到其他服务器，以便用户可以访问模式或执行预测。  
  
## <a name="in-this-section"></a>本节内容  
 本节中的主题介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据挖掘的主要功能和相关任务。  
  
-   [数据挖掘概念](../../analysis-services/data-mining/data-mining-concepts.md)  
  
-   [数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [挖掘结构（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
-   [挖掘模型（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
-   [测试和验证（数据挖掘）](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
-   [数据挖掘查询](../../analysis-services/data-mining/data-mining-queries.md)  
  
-   [数据挖掘解决方案](../../analysis-services/data-mining/data-mining-solutions.md)  
  
-   [数据挖掘工具](../../analysis-services/data-mining/data-mining-tools.md)  
  
-   [数据挖掘体系结构](../../analysis-services/data-mining/data-mining-architecture.md)  
  
-   [安全性概述（数据挖掘）](../../analysis-services/data-mining/security-overview-data-mining.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  

