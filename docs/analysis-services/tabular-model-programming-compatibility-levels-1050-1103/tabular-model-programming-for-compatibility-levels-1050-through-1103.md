---
title: Analysis Services 表格模型编程的兼容性级别为 1050年-1103年 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe2ce43ffb5d2c5be0afb39931f231d2f0d24e14
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071764"
---
# <a name="tabular-model-programming-for-compatibility-levels-1050-through-1103"></a>1050 到 1103 兼容级别的表格模型编程
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  表格模型使用关系构造对分析和报表应用程序使用的 Analysis Services 数据建模。 这些模型运行在配置用于表格模式的 Analysis Service 实例上，使用内存中分析引擎执行存储和快速表扫描（支持在请求数据时对其进行聚合和计算）。  
  
 如果表格模型数据库最能满足您的自定义 BI 解决方案的要求，则可以使用任意 Analysis Services 客户端库和编程接口将您的应用程序集成到 Analysis Services 实例上的表格模型。 若要查询和计算表格模型数据，可以在代码中使用嵌入的 MDX 或 DAX。  
  
 在早期版本的 Analysis Services，在兼容级别 1050 1103，通过特定模型中创建的表格模型以编程方式在 AMO、 ADOMD.NET、 XMLA 或 OLE DB 中使用的对象是从根本上相同表格和多维解决方案。 具体而言，定义用于多维模型的对象元数据还用于表格模型的兼容级别 1050年-1103年。  
  
 从 SQL Server 2016 开始，表格模型可以生成，或升级到 1200年或更高的兼容性级别，以便使用表格元数据来定义模型。 在此级别是根本不同的元数据和可编程性。 请参阅[表格模型编程兼容级别 1200年及更高版本](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)并[升级 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)有关详细信息。  
  
## <a name="in-this-section"></a>本节内容  
 [用于商业智能的 CSDL 批注 (CSDLBI)](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
 [了解表格对象模型在兼容级别 1050年到 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [用于商业智能的 CSDL 注释技术参考](https://docs.microsoft.com/bi-reference/csdl/technical-reference-for-bi-annotations-to-csdl)  
  

[IMDEmbeddedData 接口](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/imdembeddeddata-interface.md)


  
  
