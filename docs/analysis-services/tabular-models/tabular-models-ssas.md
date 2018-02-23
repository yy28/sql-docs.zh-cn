---
title: "表格模型 |Microsoft 文档"
ms.custom: 
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 2df607b47e4bb2a5a770e27d1bceb5a6d7e6ebbc
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="tabular-models"></a>表格模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
表格模型是在内存中或在 DirectQuery 模式下运行，并直接从后端关系数据源访问数据的 Analysis Services 数据库。 通过使用最先进的压缩算法和多线程的查询处理器，分析引擎提供快速访问，对表格模型对象和数据通过报告 Power BI 和 Excel 等的客户端应用程序。  
  
 默认设置内存中模型时，DirectQuery 是备选查询模式的模型都是过大而无法适应在内存中，或因数据易变性排除合理处理策略。 DirectQuery 实现通过支持多种不同的数据源能够处理计算的表和列在 DirectQuery 模型中，通过的 DAX 表达式。 到达后端数据库，以及如何查询的行级别安全性的内存中模型的奇偶校验导致更快的生产率的优化。
  
 表格模型是使用表格模型项目模板在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中制作而成，该模板可提供用于创建模型、表、关系和 DAX 表达式的设计图面。 你可以从多个源导入数据，然后添加关系、计算的表和列、度量值、KPI、层次结构和翻译，使模型更加丰富。  
  
 模型然后可部署到 Azure Analysis Services 或 SQL Server Analysis Services 的实例配置为表格服务器模式。 可以在 SQL Server Management Studio 中管理已部署的表格模型。 当您的模型增多时，它们可以进行优化处理分区和使用基于角色的安全性保护到行级别。  
  
## <a name="in-this-section"></a>在本节中  
 [表格模型解决方案](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)-本部分中的文章介绍创建和部署表格模型解决方案。
  
 [表格模型数据库](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)-本部分中的文章介绍管理已部署的表格模型解决方案。
  
 [表格模型数据访问](../../analysis-services/tabular-models/tabular-model-data-access.md)-本部分中的文章介绍连接部署表格模型解决方案。
  
## <a name="see-also"></a>另请参阅  
 [什么是 Analysis Services 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [比较表格和多维解决方案](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [工具和 Analysis Services 中使用的应用程序](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
