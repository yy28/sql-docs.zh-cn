---
title: 表格模型编程 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0ceb461e-12c1-44ea-97ac-b99bf308676b
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 785e4818d635d41dc27eea8fc63b62cf63e0ff92
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126624"
---
# <a name="tabular-model-programming"></a>表格模型编程
  表格模型使用关系构造对分析和报表应用程序使用的 Analysis Services 数据建模。 这些模型运行在配置用于表格模式的 Analysis Service 实例上，使用内存中分析引擎执行存储和快速表扫描（支持在请求数据时对其进行聚合和计算）。  
  
 从编程角度来看，您在 AMO、ADOMD.NET、XMLA 或 OLE DB 中处理的对象对于表格解决方案和多维解决方案而言都是基本相同的。 如果表格模型数据库最能满足您的自定义 BI 解决方案的要求，则可以使用任意 Analysis Services 客户端库和编程接口将您的应用程序集成到 Analysis Services 实例上的表格模型。 若要查询和计算表格模型数据，可以在代码中使用嵌入的 MDX 或 DAX。  
  
 本节提供有关如何以编程方式使用表格模型实体及其属性的详细信息。  
  
## <a name="in-this-section"></a>本节内容  
 [商业智能的 CSDL 批注&#40;CSDLBI&#41;](csdl-annotations-for-business-intelligence-csdlbi.md)  
  
 [了解表格对象模型](representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [用于商业智能的 CSDL 注释技术参考](conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
 [IMDEmbedded 接口](imdembeddeddata-interface.md)  
  
## <a name="see-also"></a>请参阅  
 [表格建模&#40;SSAS 表格&#41;](../tabular-models/tabular-models-ssas.md)   
 [表格模型设计器&#40;SSAS 表格&#41;](../tabular-model-designer-ssas-tabular.md)  
  
  