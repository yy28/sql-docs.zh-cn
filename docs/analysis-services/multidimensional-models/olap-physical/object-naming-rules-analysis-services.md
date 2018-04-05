---
title: 对象命名规则 (Analysis Services) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9b489ecceb4d8aeb5716708ae680999a296b5d14
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="object-naming-rules-analysis-services"></a>对象命名规则 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]本主题介绍对象命名约定，以及保留的字和字符，不能在任何对象名称，在代码中的或在脚本[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
##  <a name="bkmk_Names"></a>命名约定  
 每个对象具有**名称**和**ID**在父集合的作用域必须是唯一的属性。 例如，只要两个维度分别驻留在不同的数据库中，这两个维度就能具有相同的名称。  
  
 虽然可以手动指定**ID**是通常自动生成创建对象。 不应更改**ID**开始生成模型后。 基于整个模型的所有对象引用**ID**。 因此，更改**ID**轻松地可能会导致模型损坏。  
  
 **数据源**和**DataSourceView**对象具有明显的例外，命名约定。 **数据源**ID 可以设置为一个句点 （.），这不是唯一的为当前数据库的引用。 第二个例外情况是**DataSourceView**，这符合为定义的命名约定**数据集**对象在.NET Framework 中，其中**名称**用作标识符。  
  
 以下规则适用于**名称**和**ID**属性。  
  
-   名称不区分大小写。 同一数据库中不可同时拥有名为“sales”和“Sales”的两个多维数据集。  
  
-   对象名称中不允许使用前导空格或尾随空格，但可以在名称中嵌入空格。 前导空格和尾随空格将会被隐式删除。 这同时适用于**名称**和**ID**的对象。  
  
-   最大字符数为 100。  
  
-   对标识符的第一个字符没有特殊要求。 第一个字符可为任意有效字符。  
  
##  <a name="bkmk_reserved"></a>保留的字和字符  
 保留字用英语表示，且适用于对象名称而非标题。 如果您在对象名称中意外使用了保留字，则将发生验证错误。 对于多维和数据挖掘模型，下述保留字在任何时候都不能用于任何对象名称。  
  
 对于数据库兼容性设置为 1103 的表格模型，已针对某些对象放宽验证规则，这些对象不符合扩展字符要求和某些客户端应用程序的命名约定。 满足这些条件的数据库受更放宽的验证规则约束。 在此情况下，对象名称可以包含受限字符，并且仍可通过验证。  
  
 **保留字**  
  
-   AUX  
  
-   CLOCK$  
  
-   COM1 到 COM9（COM1、COM2、COM3 等）  
  
-   CON  
  
-   LPT1 到 LPT9（LPT1、LPT2、LPT3 等）  
  
-   NUL  
  
-   PRN  
  
-   XML 内的任何字符串的字符都不可为 NULL  
  
 **保留的字符**  
  
 下表列出了特定对象的无效字符。  
  
|Object|无效字符|  
|------------|------------------------|  
|**Server**|在对服务器对象进行命名时，请遵循 Windows 服务器命名约定。 请参阅[命名约定 (Windows)](http://msdn.microsoft.com/library/windows/desktop/ms682856\(v=vs.85\).aspx)有关详细信息。|  
|**DataSource**|: / \ * &#124; ? " () [] {} <>|  
|**级别**或**属性**|实例时都提供 SQL Server 登录名。 , ; ' ` : / \ * &#124; ? " & % $ ! + = [] {} < >|  
|**维度**或**层次结构**|实例时都提供 SQL Server 登录名。 , ; ' ` : / \ * &#124; ? " & % $ ! + = () [] {} \<,>|  
|所有其他对象|实例时都提供 SQL Server 登录名。 , ; ' ` : / \ * &#124; ? " & % $ ! + = () [] {} < >|  
  
 **： 当保留字符允许异常**  
  
 如上所述，特定模式和兼容级别的数据库可具有包含保留字符的对象名称。 对于允许使用以下扩展字符的表格数据库（1103 或更高版本），维度属性、层次结构、级别、度量值和 KPI 对象名称可包含保留字符：  
  
|服务器模式和数据库兼容级别|是否允许保留字符？|  
|--------------------------------------------------|----------------------------------|  
|MOLAP（所有版本）|是|  
|表格 - 1050|是|  
|表格 - 1100|是|  
|表格 – 1130 和更高版本|是|  
  
 数据库的默认值可为 ModelType。 默认值与多维等效，因此不支持在列名中使用保留字符。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 保留字](../../../mdx/mdx-reserved-words.md)   
 [Analysis Services 中的翻译支持](../../../analysis-services/translation-support-in-analysis-services.md)   
 [XML for Analysis 遵从性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)  
  
  
