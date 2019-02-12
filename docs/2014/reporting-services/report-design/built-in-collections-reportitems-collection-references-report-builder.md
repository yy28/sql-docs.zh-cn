---
title: ReportItems 集合引用（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 684ee8c4738b2cc46cb847820a2408365c1a5cd1
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042828"
---
# <a name="reportitems-collection-references-report-builder-and-ssrs"></a>ReportItems 集合引用（报表生成器和 SSRS）
  `ReportItems` 内置集合是来自报表项（如报表设计图面上的数据区域行或文本框）的文本框集合。 `ReportItems` 集合包括位于表头、表尾或表体的当前作用域中的文本框。 此集合在运行时由报表处理器和报表呈现器确定。 用户查看报表页面时，如果报表处理器连续组合报表数据和报表项布局元素，则当前作用域将随之变化。 可以使用 `ReportItems` 内置集合在每个页面中生成显示首项和尾项的字典样式表头。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>使用 ReportItems 值属性  
 内的项`ReportItems`集合只能有一个属性：值。 `ReportItems` 项的值可用于显示或计算报表中其他字段的数据。 若要访问当前文本框的值，可以使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 内置全局 Me.Value 或仅使用 Value。 在报表函数（如 First）和聚合函数中使用完全限定语法。  
  
 例如：  
  
-   此表达式放置在文本框中时，显示名为 `Textbox1` 的 `ReportItem` 文本框的值：  
  
     `=ReportItems!Textbox1.Value`  
  
-   此表达式放置在`ReportItem`文本框 Color 属性中，以黑色显示文本时的值为 > 0; 否则，以红色显示值：  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   此表达式放置在表头或表尾的文本框中时，显示所呈现的报表每一页中名为 `LastName`的文本框的第一个值：  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>字典样式表头表达式  
 可以创建一个表头，显示此页第一个客户和最后一个客户。 因为在一个表达式中，表头中的文本框只能引用一次 `ReportItems` 内置集合，所以需要在表头添加两个文本框：一个用于第一个客户名称 (`=First(ReportItems!textboxLastName.Value`)，另一个用于最后一个客户名称 (`=Last(ReportItems!textboxLastName.Value`)。  
  
 在表头或表尾部分，只有当前页中的文本框才能作为 `ReportItems` 集合的成员。 例如，在多页数据区域中，如果 `ReportItems!textboxLastName.Value` 引用一个只显示在首页的文本框，则可以在首页看到一个值，其他页则显示 **#Error** ，表明该表达式不能按本文所述进行计算。  
  
## <a name="scope-for-the-reportitems-collection"></a>ReportItems 集合的作用域  
 处理报表时，文本框所在数据集、数据区域和组关联的上下文将计算表体或数据区域中的所有文本框。 对 `ReportItems` 集合的引用的作用域为当前作用域或高于当前作用域的任何点。  
  
 例如，位于父组行的文本框不能包含引用子组行的文本框名称的表达式。 此类表达式不会解析报表中的值，因为子行文本框超出了作用域。 有关详细信息，请参阅 [聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)。  
  
## <a name="see-also"></a>请参阅  
 [表达式中的内置集合（报表生成器和 SSRS）](built-in-collections-in-expressions-report-builder.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [Reporting Services 中的分页（报表生成器和 SSRS）](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
