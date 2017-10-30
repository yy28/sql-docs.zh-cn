---
title: "组表达式示例 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data [Reporting Services], grouping
- grouping data
- expressions [Reporting Services], adding
- groups [Reporting Services], expressions
ms.assetid: 34cd0249-fc74-4cf2-ba11-7b072992bfd2
caps.latest.revision: 24
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cbb4f5f3af2a8986fdc7384ad4da1740f2be6638
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="group-expression-examples-report-builder-and-ssrs"></a>组表达式示例（报表生成器和 SSRS）
  在数据区域中，可以按单个字段对数据进行分组，也可以创建标识要对其进行分组的数据的更复杂表达式。 复杂表达式包含对多个字段或参数、条件语句或自定义代码的引用。 定义数据区域组时，可以将这些表达式添加到 **“组”** 属性中。 有关详细信息，请参阅[在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 若要合并两个或多个基于简单字段表达式的组，请将每个字段都添加到组定义中的组表达式列表中。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="examples-of-group-expressions"></a>组表达式示例  
 下表提供了可用于定义组的组表达式示例。  
  
|Description|表达式|  
|-----------------|----------------|  
|按 `Region` 字段分组。|`=Fields!Region.Value`|  
|按姓氏和名字分组。|`=Fields!LastName.Value`<br /><br /> `=Fields!FirstName.Value`|  
|按姓氏的第一个字母分组。|`=Fields!LastName.Value.Substring(0,1)`|  
|按参数分组（基于用户选择）。<br /><br /> 在此示例中，参数 `GroupBy` 必须基于可提供有效分组依据选项的可用值列表。|`=Fields(Parameters!GroupBy.Value).Value`|  
|按三个不同年龄范围分组：<br /><br /> “小于 21”、“21 到 50”和“大于 50”。|`=IIF(First(Fields!Age.Value)<21,"Under 21",(IIF(First(Fields!Age.Value)>=21 AND First(Fields!Age.Value)<=50,"Between 21 and 50","Over 50")))`|  
|按多个年龄范围分组。 本示例演示了一段以 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET 编写的自定义代码，此段代码可返回下列年龄范围的字符串：<br /><br /> 小于等于 25<br /><br /> 26 到 50<br /><br /> 51 到 75<br /><br /> 大于 75|`=Code.GetRangeValueByAge(Fields!Age.Value)`<br /><br /> 自定义代码：<br /><br /> `Function GetRangeValueByAge(ByVal age As Integer) As String`<br /><br /> `Select Case age`<br /><br /> `Case 0 To 25`<br /><br /> `GetRangeValueByByAge = "25 or Under"`<br /><br /> `Case 26 To 50`<br /><br /> `GetRangeValueByByAge = "26 to 50"`<br /><br /> `Case 51 to 75`<br /><br /> `GetRangeValueByByAge = "51 to 75"`<br /><br /> `Case Else`<br /><br /> `GetRangeValueByByAge = "Over 75"`<br /><br /> `End Select`<br /><br /> `Return GetRangeValueByByAge`<br /><br /> `End Function`|  
  
## <a name="see-also"></a>另请参阅  
 [筛选器、 组中，以及对数据进行排序和 #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [自定义代码和在报表设计器 &#40; 中的表达式的程序集引用SSRS &#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)  
  
  

