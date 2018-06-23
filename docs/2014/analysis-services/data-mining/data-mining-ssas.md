---
title: 数据挖掘 (SSAS) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b118f03580aeb0053203cd2535bafecd1649ccb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126197"
---
# <a name="data-mining-ssas"></a>数据挖掘 (SSAS)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 为合并数据挖掘的解决方案提供一个集成的平台。 您可以使用关系数据或多维数据集数据创建具有预测分析功能的商业智能解决方案。  
  
## <a name="benefits-of-data-mining"></a>数据挖掘的优点  
 数据挖掘使用精心研究的统计原则来发现您的数据中的模式，帮助您针对复杂问题作出明智的决策。 通过将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的数据挖掘算法应用于您的数据，您可以预测趋势、标识模式、创建规则和建议、分析复杂数据集中的事件顺序以及洞察新情况。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的数据挖掘不仅功能强大和易于访问，并且与许多人在进行分析和报告工作时喜欢使用的工具集成在一起。 通过查看本节中提供的链接，您可以获取在开始学习数据挖掘时需要掌握的丰富背景信息。  
  
## <a name="key-data-mining-features"></a>关键数据挖掘功能  
 SQL Server 提供了以下功能来支持集成的数据挖掘解决方案：  
  
-   多个数据源：您无需创建数据仓库或 OLAP 多维数据集就可以执行数据挖掘。 你可以使用来自外部提供程序、电子表格甚至文本文件的表格格式数据。 此外，您还可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中轻松地挖掘创建的 OLAP 多维数据集。 但是，不能使用内存中数据库的数据。  
  
-   集成的数据清理、数据管理和 ETL：Data Quality Services 提供了用于探查和清理数据的高级工具。 Integration Services 可用于生成 ETL 进程以用于清理数据，并且还用于生成、处理、定型和更新模型。  
  
-   多个可自定义的算法：除了提供聚类分析、神经网络和决策树之类的算法之外，该平台还支持开发您自己的自定义插件算法。  
  
-   模型测试基础结构：使用重要的统计工具（例如交叉验证、分类矩阵、提升图和散点图）测试您的模型和数据集。 轻松创建和管理测试和定型集。  
  
-   查询和钻取：创建预测查询、检索模型模式和统计信息以及钻取到事例数据。  
  
-   客户端工具：除了 SQL Server 提供的开发和设计工具之外，您还可以使用 Excel 数据挖掘外接程序来创建、查询和浏览模型。 或者，创建自定义的客户端，包括 Web 服务。  
  
-   脚本语言支持和托管 API：所有数据挖掘对象都是完全可编程的。 可通过用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的 MDX、XMLA 或 PowerShell 扩展插件来撰写脚本。 使用数据挖掘扩展插件 (DMX) 语言来进行快速查询和脚本撰写。  
  
-   安全性和部署：通过 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供基于角色的安全性，包括用于钻取到模型和结构数据的单独权限。 轻松地将模型部署到其他服务器，以便用户可以访问模式或执行预测。  
  
## <a name="in-this-section"></a>本节内容  
 本节中的主题介绍 SQL Server 数据挖掘的主要功能和相关任务。  
  
-   [数据挖掘概念](data-mining-concepts.md)  
  
-   [数据挖掘算法&#40;Analysis Services-数据挖掘&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [挖掘结构&#40;Analysis Services-数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)  
  
-   [挖掘模型&#40;Analysis Services-数据挖掘&#41;](mining-models-analysis-services-data-mining.md)  
  
-   [测试和验证&#40;数据挖掘&#41;](testing-and-validation-data-mining.md)  
  
-   [数据挖掘查询](data-mining-queries.md)  
  
-   [数据挖掘解决方案](data-mining-solutions.md)  
  
-   [数据挖掘工具](data-mining-tools.md)  
  
-   [数据挖掘体系结构](data-mining-architecture.md)  
  
-   [安全概述&#40;数据挖掘&#41;](security-overview-data-mining.md)  
  
  