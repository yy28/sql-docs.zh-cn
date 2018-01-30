---
title: "表格模型 |Microsoft 文档"
ms.custom: 
ms.date: 01/29/2018
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
ms.openlocfilehash: edeea89c1d767364f4f087d0f4b2e6d566895c52
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2018
---
# <a name="tabular-models"></a>表格模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]表格模型是 Analysis Services 数据库，内存中或在 DirectQuery 模式下，从后端关系数据源访问数据直接运行。  
  
 默认模式为内存中。 使用最先进的压缩算法和多线程的查询处理器，分析引擎提供快速访问对表格模型对象和数据通过报告 Power BI 和 Excel 等的客户端应用程序。  
  
 当模型因过大而无法适应内存大小，或因数据易变性而排除合理处理策略时，DirectQuery 是备选查询模式。 在此版本中，DirectQuery 通过支持更多数据源提升了与内存中模型的对等性，能够在 DirectQuery 模型中处理计算的表和列，通过连接后端数据库的 DAX 表达式实现了行级别安全性，并通过查询优化在旧版的基础上加快了吞吐量。
  
 表格模型是使用表格模型项目模板在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中制作而成，该模板可提供用于创建模型、表、关系和 DAX 表达式的设计图面。 你可以从多个源导入数据，然后添加关系、计算的表和列、度量值、KPI、层次结构和翻译，使模型更加丰富。  
  
 模型然后可部署到 Azure Analysis Services 或 SQL Server Analysis Services 的实例配置为表格服务器模式。 就像多维模型一样，可以在 SQL Server Management Studio 中管理已部署的表格模型。 还可以对它们进行分区以便优化处理，并使用基于角色的安全性保护行级数据安全。  
  
## <a name="in-this-section"></a>在本节中  
 [表格模型解决方案](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)-此部分中的主题描述了创建和部署表格模型解决方案。
  
 [表格模型数据库](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)-本部分中的主题介绍管理已部署的表格模型解决方案。
  
 [表格模型数据访问](../../analysis-services/tabular-models/tabular-model-data-access.md)-此部分中的主题描述连接部署表格模型解决方案。
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [比较表格和多维解决方案](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [工具和 Analysis Services 中使用的应用程序](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
