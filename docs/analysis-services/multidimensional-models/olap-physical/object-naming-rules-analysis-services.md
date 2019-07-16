---
title: 对象命名规则 (Analysis Services) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7267097b1a06cb44c801ed20cbfd206c330328ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68165459"
---
# <a name="object-naming-rules-analysis-services"></a>对象命名规则 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  本主题介绍对象命名约定，以及无法在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的任何对象名称、代码或脚本中使用的保留字和字符。  
  
##  <a name="bkmk_Names"></a> 命名约定  
 每个对象具有**名称**并**ID**父集合的作用域中必须是唯一的属性。 例如，只要两个维度分别驻留在不同的数据库中，这两个维度就能具有相同的名称。  
  
 虽然可以手动指定**ID**是通常自动生成时创建对象。 您应永远不会更改**ID**开始生成模型后。 基于整个模型的所有对象引用**ID**。 因此，更改**ID**可能很容易导致模型损坏。  
  
 **数据源**并**DataSourceView**对象具有明显的例外，命名约定。 **数据源**ID 可以设置为单个点 （.），它不是唯一的作为对当前数据库的引用。 第二个例外是**DataSourceView**，它遵循为定义的命名约定**数据集**对象在.NET Framework 中，其中**名称**用作标识符。  
  
 以下规则适用于**名称**并**ID**属性。  
  
-   名称不区分大小写。 不能具有名为"sales"的多维数据集和另一个名为"Sales"同一数据库中。  
  
-   对象名称中不允许使用前导空格或尾随空格，但可以在名称中嵌入空格。 前导空格和尾随空格将会被隐式删除。 这同时适用于**名称**并**ID**的对象。  
  
-   最大字符数为 100。  
  
-   对标识符的第一个字符没有特殊要求。 第一个字符可为任意有效字符。  
  
##  <a name="bkmk_reserved"></a> 保留的字和字符  
 保留字用英语表示，且适用于对象名称而非标题。 如果您在对象名称中意外使用了保留字，则将发生验证错误。 对于多维和数据挖掘模型，在任何对象名称中任何时候都不能使用下面描述的保留字。  
  
 对于表格模型（其中的数据库兼容性设置为 1103），已放宽了针对某些对象、扩展字符的不合规要求和某些客户端应用程序命名约定的验证规则。 满足这些条件的数据库受更放宽的验证规则约束。 在这种情况下，对象名称可以包含受限制的字符且能够通过验证。  
  
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
|**Server**|在对服务器对象进行命名时，请遵循 Windows 服务器命名约定。 请参阅[命名约定 (Windows)](/windows/desktop/DNS/naming-conventions)有关详细信息。|  
|**DataSource**|: / \ * &#124; ? "（) [] {} <>|  
|**级别**或**属性**|. , ; ' ` : / \ * &#124; ? "& %$ ！ + = [] {} < >|  
|**维度**或**层次结构**|. , ; ' ` : / \ * &#124; ? "& %$ ！ + = （) [] {} \<，>|  
|所有其他对象|. , ; ' ` : / \ * &#124; ? "& %$ ！ + = （) [] {} < >|  
  
 **异常：如果允许使用保留字符**  
  
 如前所述，特定模式和兼容级别的数据库可以具有包含保留字符的对象名称。 对于允许使用扩展字符的表格数据库（1103 或更高），维度属性、层次结构、级别、度量值和 KPI 对象名称可以包含保留字符：  
  
|服务器模式和数据库兼容级别|是否允许保留字符？|  
|--------------------------------------------------|----------------------------------|  
|MOLAP（所有版本）|否|  
|表格 - 1050|否|  
|表格 - 1100|否|  
|表格-1130年和更高版本|是|  
  
 数据库可以拥有默认的 ModelType。 默认值等效于多维的，因此不支持在列名称中使用保留字符。  
  
## <a name="see-also"></a>请参阅  
 [MDX 保留字](../../../mdx/mdx-reserved-words.md)   
 [Analysis Services 中的翻译支持](../../../analysis-services/translation-support-in-analysis-services.md)   
 [XML for Analysis 遵从性&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-compliance-xmla)  
  
  
