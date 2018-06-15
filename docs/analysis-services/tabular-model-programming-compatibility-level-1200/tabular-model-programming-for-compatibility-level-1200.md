---
title: 兼容级别 1200年的表格模型编程 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e0bfc84806e44ef05312da9d15d1afaa7dd9754
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039141"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>表格模型编程的兼容性级别 1200年及更高版本
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
从开始兼容级别 1200年，用于使用表格元数据描述模型结构，作为表格模型对象的描述符替换历史多维元数据。 表、 列和关系的元数据是表、 列中，和关系，而不是多维的等效项 （维度和属性）。  
  
你可以创建新模型的兼容性级别 1200年或更高版本通过使用 Microsoft.AnalysisServices.Tabular Api，最新版本的 SQL Server Data Tools (SSDT)，或通过更改**CompatibilityLevel**的现有表格若要升级它 （也在 SSDT 中完成） 的模型。 这样将模型绑定到较新版本的服务器、 工具和编程接口。   
  
升级现有的表格解决方案是建议，但不是要求。 可用作现有脚本和自定义解决方案，访问或管理表格模型或数据库的是。 在该级别使用提供的功能的 SQL Server 2016 中完全支持更早版本的兼容性级别。 Azure Analysis Services 仅支持兼容性级别 1200年或更高版本。
  
 不同的代码和脚本，下面总结了，将需要新的表格模型。  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>作为表格元数据构造的对象模型定义  
 在通过 JSON 中公开表格对象模型为 1200年或更高版本的模型[表格模型脚本语言](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)和 AMO 数据定义语言通过新的命名空间，通过[Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>表格模型和数据库的脚本  
 TMSL 是 JSON 脚本语言中的表格模型，使用支持创建、 读取、 更新和删除操作。 你可以刷新数据通过 TMSL 和调用附加、 detatch、 备份、 还原数据库操作并同步。  
  
 AMO PowerShell 接受 TMSL 脚本作为输入。  
  
 请参阅[表格模型脚本语言&#40;TMSL&#41;引用](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)和[Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md)有关详细信息。  
  
## <a name="query-languages"></a>查询语言  
 为所有的表格模型支持 DAX 和 MDX。  
  
## <a name="expression-language"></a>表达式语言  
 筛选器和用于创建计算的对象，包括度量值和 Kpi，表达式是 DAX 中表述的。 请参阅[了解表格模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)和[数据分析表达式&#40;DAX&#41; Analysis Services 中](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)。  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>表格模型和数据库的托管的代码  
 AMO 包括新的命名空间，Microsoft.AnalysisServices.Tabular，以编程方式使用的模型。 请参阅[Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)有关详细信息。  
  
> [!NOTE]  
>  Analysis Services 管理对象 (AMO)、 ADOMD.NET 和表格对象模型 (TOM) 客户端库现在针对.NET 4.0 运行时。   
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 开发人员文档](../../analysis-services/analysis-services-developer-documentation.md)   
 [表格模型编程的兼容性级别 1050年通过 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [技术参考](../../analysis-services/powershell/technical-reference-ssas.md)[升级 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [表格模型和数据库的兼容级别](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
