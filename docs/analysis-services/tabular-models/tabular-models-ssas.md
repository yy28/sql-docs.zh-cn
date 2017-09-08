---
title: "表格模型 (SSAS) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f1f324d1ba1b4ba9299c4d29e565d09d1f71fb2c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-modeling-ssas"></a>表格建模 (SSAS)
  表格模型是在内存中或在 DirectQuery 模式下运行，并直接从后端关系数据源访问数据的 Analysis Services 数据库。  
  
 默认模式为内存中。 内存中分析引擎使用最先进的压缩算法和多线程查询处理器，通过报告客户端应用程序（如 Microsoft Excel 和 Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]），可以提供对表格模型对象和数据的快速访问。  
  
 当模型因过大而无法适应内存大小，或因数据易变性而排除合理处理策略时，DirectQuery 是备选查询模式。 在此版本中，DirectQuery 通过支持更多数据源提升了与内存中模型的对等性，能够在 DirectQuery 模型中处理计算的表和列，通过连接后端数据库的 DAX 表达式实现了行级别安全性，并通过查询优化在旧版的基础上加快了吞吐量。
  
 表格模型是使用表格模型项目模板在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中制作而成，该模板可提供用于创建模型、表、关系和 DAX 表达式的设计图面。 你可以从多个源导入数据，然后添加关系、计算的表和列、度量值、KPI、层次结构和翻译，使模型更加丰富。  
  
 接下来，可以将模型部署到客户端报告应用程序可以连接到的配置了表格服务器模式的 Analysis Services 实例。 可以在 SQL Server Management Studio 中管理已部署的模型，就像管理多维模型一样。 还可以对它们进行分区以便优化处理，并使用基于角色的安全性保护行级数据安全。  
  
## <a name="in-this-section"></a>本节内容  
 [表格模型解决方案（SSAS 表格）](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)  - 本部分中的主题说明了如何创建和部署表格模型解决方案。
  
 [表格模型数据库（SSAS 表格）](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  - 本部分中的主题说明了如何管理部署的表格模型解决方案。
  
 [表格模型数据访问](../../analysis-services/tabular-models/tabular-model-data-access.md)  - 本部分中的主题说明了如何连接部署的表格模型解决方案。
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [比较表格和多维解决方案 (SSAS)](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [工具和 Analysis Services 中使用的应用程序](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery 模式（SSAS 表格）](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis Services 中表格模型的兼容级别](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
