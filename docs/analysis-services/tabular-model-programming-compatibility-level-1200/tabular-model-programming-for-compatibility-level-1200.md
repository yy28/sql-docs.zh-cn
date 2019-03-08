---
title: Analysis Services 表格模型编程兼容级别 1200年的 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7493c09964db2e0a8cbd17c6a2278dd554a2dcc
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579447"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>表格模型编程兼容级别 1200 及更高
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
从开始兼容性级别 1200年，表格元数据用于描述模型构造，为表格模型对象的描述符替换历史多维元数据。 表、 列和关系的元数据是表、 列和关系，而不是多维的等效项 （维度和属性）。  
  
您可以创建新模型兼容级别 1200年或更高版本使用 Microsoft.AnalysisServices.Tabular Api、 最新版本的 SQL Server Data Tools (SSDT)，或通过更改**CompatibilityLevel**的现有表格若要升级它 （也在 SSDT 中完成） 的模型。 执行此操作将在模型绑定到较新版本的服务器、 工具和编程接口。   
  
升级现有表格解决方案建议但不是必需的。 可用作现有脚本和自定义解决方案的访问或管理表格模型或数据库-是。 在 SQL Server 2016 中使用该级别提供的功能完全支持更低的兼容性级别。 Azure Analysis Services 仅支持兼容性级别 1200年或更高。
  
 新的表格模型将需要不同的代码和脚本，总结如下。  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>作为表格元数据构造的对象模型定义  
 表格对象模型为 1200年或更高版本的模型通过 JSON 中公开[表格模型脚本语言](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)并通过新的命名空间在 AMO 数据定义语言通过[Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>表格模型和数据库的脚本  
 TMSL 是 JSON 脚本语言中的表格模型中，使用支持创建、 读取、 更新和删除操作。 可以刷新数据通过 TMSL 和调用数据库操作，用于附加、 detatch、 备份、 还原和同步。  
  
 AMO PowerShell 接受 TMSL 脚本作为输入。  
  
 请参阅[表格模型脚本语言&#40;TMSL&#41;引用](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference)并[Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md)有关详细信息。  
  
## <a name="query-languages"></a>查询语言  
 适用于所有表格模型支持 DAX 和 MDX。  
  
## <a name="expression-language"></a>表达式语言  
 筛选器和表达式，用来创建计算的对象，包括度量值和 Kpi，进行公式化在 DAX 中表示。 请参阅[了解表格模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)并[数据分析表达式&#40;DAX&#41;在 Analysis Services 中](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)。  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>托管的代码的表格模型和数据库  
 AMO 包含新的命名空间，Microsoft.AnalysisServices.Tabular，用于以编程方式使用模型。 请参阅[Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)有关详细信息。  
  
> [!NOTE]  
>  Analysis Services 管理对象 (AMO)、 ADOMD.NET 和表格对象模型 (TOM) 客户端库现在面向.NET 4.0 运行时。   
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 开发人员文档](../../analysis-services/analysis-services-developer-documentation.md)   
 [表格模型编程兼容级别 1050年到 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [技术参考](../../analysis-services/powershell/technical-reference-ssas.md)[升级 Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [兼容性级别的表格模型和数据库](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
