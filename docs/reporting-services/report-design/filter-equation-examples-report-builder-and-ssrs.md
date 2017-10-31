---
title: "筛选器公式示例 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtering data [Reporting Services], filter equation examples
ms.assetid: 66bec93d-7c3b-4d4a-8cb6-7a7bb2f34ec6
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6bbd95ac20afbeb00b331efa13492a0036fff20
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="filter-equation-examples-report-builder-and-ssrs"></a>筛选器公式示例（报表生成器和 SSRS）
  若要创建筛选器，必须指定一个或多个筛选器公式。 筛选器公式包括表达式、数据类型、运算符和值。 本主题提供了常用筛选器的示例。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>筛选器示例  
 下表显示使用不同数据类型和不同运算符的筛选器公式的示例。 比较的范围由将为其定义筛选器的报表项确定。 例如，对于为数据集定义的筛选器， **TOP % 10** 表示数据集中前 10% 的值；对于为组定义的筛选器， **TOP % 10** 表示组中前 10% 的值。  
  
|简单表达式|数据类型|运算符|“值”|Description|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**Integer**|**>**|`7`|包括大于 7 的数据值。|  
|`[SUM(Quantity)]`|**Integer**|**前 N 个**|`10`|包括前 10 个数据值。|  
|`[SUM(Quantity)]`|**Integer**|**前 %**|`20`|包括前 20% 的数据值。|  
|`[Sales]`|**Text**|**>**|`=CDec(100)`|包括大于 $100 的 System.Decimal（SQL“money”数据类型）类型的所有值。|  
|`[OrderDate]`|**DateTime**|**>**|`2008-01-01`|包括从 2008 年 1 月 1 日到当前日期的所有日期。|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|包括从 2008 年 1 月 1 日到 2008 年 2 月 1 日（含此日）的日期。|  
|`[Territory]`|**Text**|**LIKE**|`*east`|以“east”结尾的所有区域名称。|  
|`[Territory]`|**Text**|**LIKE**|`%o%th*`|名称开头包括“North”和“South”的所有区域名称。|  
|`=LEFT(Fields!Subcat.Value,1)`|**Text**|**IN**|`B, C, T`|以字母 B、 C 或 T 开头的所有子类别值。|  
  
## <a name="see-also"></a>另请参阅  
 [报表参数 &#40;报表生成器和报表设计器 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [添加数据集筛选器、 数据区域筛选器和组筛选器 （&） #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [表达式 &#40; 中的数据类型报表生成器和 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [在报表 &#40; 中使用表达式报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
