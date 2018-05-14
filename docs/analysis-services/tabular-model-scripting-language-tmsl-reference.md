---
title: 表格模型脚本语言 (TMSL) 参考 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 713fecbb367ac4717604c14b6f23baab905a993f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-model-scripting-language-tmsl-reference"></a>表格模型脚本语言 (TMSL) 参考
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  表格模型脚本语言 (TMSL) 是在兼容级别 1200年或更高版本的 Analysis Services 表格模型数据库的命令和对象模型定义语法。 TMSL 与 Analysis Services 通信通过 XMLA 协议，其中[XMLA。执行](../analysis-services/xmla/xml-elements-methods-execute.md)方法同时接受基于 JSON 的**语句**中为中的传统的基于 XML 的脚本或 TMSL 脚本[Analysis Services 脚本语言&#40;的 XMLA ASSL&#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 TMSL 的要素包括：  
  
-   基于表格模型语义表格元数据。 表格模型组成表、 列和关系。 采用 TMSL 的等效对象定义对现在，因此，表、 列、 关系和等。  
  
     新的元数据引擎支持这些定义。  
  
-   对象定义组织为 JSON 而不是 XML。  
  
 除了负载格式的方法 （在 JSON 或 XML） TMSL 和 ASSL 在功能上等效中如何提供命令和 XMLA 方法用于服务器通信和数据传输到元数据。  
  
## <a name="how-to-use-tmsl"></a>如何使用 TMSL  
 浏览 TMSL 脚本的最简单方法使用 CREATE、 ALTER、 DELETE 或进程命令在 SQL Server Management Studio (SSMS) 在你已经知道的模型上。 假定你使用的现有模型，请记住先升级到兼容性级别为 1200年或更高版本。  
  
1.  找到你想要使用的命令：[中表格模型脚本语言命令&#40;TMSL&#41;](../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)  
  
2.  检查命令中使用的对象的对象定义引用：[表格模型脚本语言中的对象定义&#40;TMSL&#41;](../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)  
  
3.  选择用于提交 TMSL 脚本方法：  
  
    -   Management Studio 中的 XMLA 窗口  
  
    -   **调用 ascmd**通过 AMO PowerShell ([Invoke ASCmd cmdlet](../analysis-services/powershell/invoke-ascmd-cmdlet.md))  
  
    -   [Analysis Services 执行 DDL 任务](../integration-services/control-flow/analysis-services-execute-ddl-task.md)SSIS 中。  
  
## <a name="model-definition-schema"></a>模型定义架构  
 以下屏幕截图显示架构，折叠以显示主要对象的缩写的版本。  
  
 ![SSAS_TabularMetadata](../analysis-services/media/ssas-tabularmetadata.JPG "SSAS_TabularMetadata")  
  
## <a name="scripting-languages-in-analysis-services"></a>Analysis Services 中的脚本语言  
 Analysis Services 支持 ASSL 和 TMSL 脚本语言。 仅在 1200年兼容级别或更高版本创建表格模型中将介绍 TMS JSON 格式。  
  
 [Analysis Services 脚本语言&#40;的 XMLA ASSL&#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)第一种脚本语言，并且仍是多维模型和表格模型的较低的兼容性级别 （1100年或 1103年） 唯一的脚本语言。 在 ASSL，110 x 处的表格模型所述多维条款，如**多维数据集**（适用于模型） 和**measuregroup** （适用于一个表）。  
  
> [!NOTE]  
>  在 [SQL Server Data Tools (SSDT)，你可以升级的较早的版本表格模型使用通过向上切换 TMSL 其**CompatibilityLevel**为 1200年或更高版本。 请记住该升级是不可逆。 在升级之前，备份您的模型，以防需要原始版本更高版本。  
  
 下表是 Analysis Services 数据模型的脚本语言矩阵跨不同版本，在特定的兼容性级别。  

||||||  
|-|-|-|-|-|  
|**版本**|**多维**|**表格 110 x**|**表格 1200**| **表格 1400** |
|Azure Analysis Services|不适用|不适用|TMSL|TMSL| 
|SQL Server 2017|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2016|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2014|ASSL|ASSL|不适用|不适用|   
|SQL Server 2012|ASSL|ASSL|不适用|不适用|  

  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 中的表格模型的兼容性级别](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 脚本语言&#40;的 XMLA ASSL&#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [确定 Analysis Services 实例的服务器模式](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
