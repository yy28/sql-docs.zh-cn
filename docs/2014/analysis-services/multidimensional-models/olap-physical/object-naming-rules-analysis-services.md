---
title: 对象命名规则 (Analysis Services) |Microsoft Docs
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
helpviewer_keywords:
- objects [Analysis Services], naming
ms.assetid: b338a60d-4802-4b68-862a-6dc6a3f75e48
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c59c295c627c311aaec574ecd04b153004c3c926
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202077"
---
# <a name="object-naming-rules-analysis-services"></a>对象命名规则 (Analysis Services)
  本主题介绍对象命名约定，以及不能在任何对象名称、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的代码或脚本中使用的保留字和字符。  
  
##  <a name="bkmk_Names"></a> 命名约定  
 每个对象都拥有一个 `Name` 和 `ID` 属性，该属性在父集合的范围内必须是唯一的。 例如，只要两个维度分别驻留在不同的数据库中，这两个维度就能具有相同的名称。  
  
 尽管您可以手动指定 `ID`，不过此属性通常是在创建对象时自动生成的。 在开始构建模型之后，您绝不应更改 `ID`。 模型中的所有对象引用都基于 `ID`， 因此，更改 `ID` 很容易导致模型损坏。  
  
 `DataSource` 和 `DataSourceView` 对象是命名约定的两个值得注意的例外。 `DataSource` ID 可以设置为不具唯一性的一个点 (.)，这表示对当前数据库的引用。 另一个例外是 `DataSourceView`，它遵循的是针对 .NET Framework 中的 `DataSet` 对象定义的命名约定（其中的 `Name` 用作标识符）。  
  
 以下规则适用于 `Name` 和 `ID` 属性。  
  
-   名称不区分大小写。 同一数据库中不可同时拥有名为“sales”和“Sales”的两个多维数据集。  
  
-   对象名称中不允许使用前导空格或尾随空格，但可以在名称中嵌入空格。 前导空格和尾随空格将会被隐式删除。 这适用于对象的 `Name` 和 `ID`。  
  
-   最大字符数为 100。  
  
-   对标识符的第一个字符没有特殊要求。 第一个字符可为任意有效字符。  
  
##  <a name="bkmk_reserved"></a> 保留的字和字符  
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
|`Server`|在对服务器对象进行命名时，请遵循 Windows 服务器命名约定。 请参阅[命名约定 (Windows)](http://msdn.microsoft.com/library/windows/desktop/ms682856\(v=vs.85\).aspx)有关详细信息。|  
|`DataSource`|: / \ * &#124; ? "（) [] {} <>|  
|`Level` 或 `Attribute`|实例时都提供 SQL Server 登录名。 , ; ' ` : / \ * &#124; ? " & % $ ! + = [] {} \< >|  
|`Dimension` 或 `Hierarchy`|实例时都提供 SQL Server 登录名。 , ; ' ` : / \ * &#124; ? " & % $ ! + = （) [] {} \<，>|  
|所有其他对象|实例时都提供 SQL Server 登录名。 , ; ' ` : / \ * &#124; ? " & % $ ! + = () [] {} \< >|  
  
 **异常： 当允许保留字符的**  
  
 如上所述，特定模式和兼容级别的数据库可具有包含保留字符的对象名称。 对于允许使用以下扩展字符的表格数据库（1103 或更高版本），维度属性、层次结构、级别、度量值和 KPI 对象名称可包含保留字符：  
  
|服务器模式和数据库兼容级别|是否允许保留字符？|  
|--------------------------------------------------|----------------------------------|  
|MOLAP（所有版本）|“否”|  
|表格 - 1050|“否”|  
|表格 - 1100|“否”|  
|表格 – 1130 和更高版本|是|  
  
 数据库的默认值可为 ModelType。 默认值与多维等效，因此不支持在列名中使用保留字符。  
  
## <a name="see-also"></a>请参阅  
 [MDX 保留字](/sql/mdx/mdx-reserved-words)   
 [翻译&#40;Analysis Services&#41;](../../../analysis-services/translations-analysis-services.md)   
 [XML for Analysis 遵从性&#40;XMLA&#41;](../../xmla/xml-for-analysis-compliance-xmla.md)  
  
  
