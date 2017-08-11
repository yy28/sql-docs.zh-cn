---
title: "表达式使用在报表 （报表生成器和 SSRS） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
caps.latest.revision: 59
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 546817a006d06b1acbea5962cc1a3230867e111e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>在报表中使用表达式（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，可以在整个报表定义中使用表达式来指定或计算以下各项的值：参数、查询、筛选器、报表项属性、组和排序定义、文本框属性、书签、文档结构图、动态页眉和页脚内容、图像以及动态数据源定义。 本主题提供了一些可在其中使用表达式更改报表内容或外观的示例。 此列表并不全面。 你可以在一个对话框，显示表达式设置任何属性的表达式 (**fx**) 按钮，或者在下拉列表，显示**\<表达式...>**。  
  
 表达式可以是简单的，也可以是复杂的。 “简单表达式” 包含对单个数据集字段、参数或内置字段的引用。 复杂表达式可以包含多个内置引用、运算符和函数调用。 例如，复杂表达式可能包含应用于“销售量”字段的 Sum 函数。  
  
 表达式以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]语言编写。 表达式以等号 (=) 开头，后跟对内置集合（如数据集字段和参数）、常量、函数和运算符的引用组合。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a> 使用简单表达式  
 简单表达式以前后加方括号的形式显示在设计图面和对话框中。例如，某个数据集字段显示为 `[ProductID]`。 将字段从数据集拖到文本框中时，会自动创建简单表达式。 会创建一个占位符，并且该表达式将定义基础值。 还可以在设计图面或对话框中的数据区域单元格或文本框中直接键入表达式，例如 `[ProductID]`。  
  
 下表列出了简单表达式的用法示例： 该表介绍了功能、要设置的属性、通常用于设置该属性的对话框以及属性的值。 与其他表达式一样，您可以在设计图面上、对话框或“属性”窗格中直接键入简单表达式，也可以在“表达式”对话框中编辑简单表达式。  
  
|功能|属性、上下文和对话框|属性值|  
|-------------------|---------------------------------------|--------------------|  
|指定要在文本框中显示的数据集字段。|文本框中占位符的 Value 属性。 使用 **“占位符属性”**对话框 -&gt;“常规”。|`[Sales]`|  
|组的聚合值。|与 Tablix 组相关联的行中占位符的 Value 属性。 使用 **“文本框属性”**对话框。|`[Sum(Sales)]`|  
|包含页码。|位于页眉的文本框中占位符的 Value 属性。 使用 **“文本框属性”**对话框 -&gt;“常规”。|`[&PageNumber]`|  
|显示所选参数值。|设计图面上的文本框中占位符的 Value 属性。 使用 **“文本框属性”**对话框 -&gt;“常规”。|`[@SalesThreshold]`|  
|指定数据区域的组定义。|Tablix 组中的组表达式。 使用 **“Tablix 组属性”**对话框 -&gt;“常规”。|`[Category]`|  
|从表中排除特定字段值。|Tablix 中的筛选器公式。 使用 **“Tablix 属性”**对话框 -&gt;“筛选器”。|有关数据类型，请选择 **Integer**。<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|只包含组筛选器的特定值。|Tablix 组中的筛选器公式。 使用 **“Tablix 组属性”**对话框 -&gt;“筛选器”。|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|从数据集中排除多个字段的特定值。|Tablix 中组的筛选器公式。 使用 **“Tablix 属性”**对话框 -&gt;“筛选器”。|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|基于表中的现有字段指定排序顺序。|Tablix 中的排序表达式。 使用 **“Tablix 属性”**对话框 -&gt;“排序”。|`[SizeSortOrder]`|  
|将查询参数链接到报表参数。|数据集中的参数集合。 使用 **“数据集属性”**对话框 -&gt;“参数”。|`[@Category]`<br /><br /> `[@Category]`|  
|将参数从主报表传递到子报表。|子报表中的参数集合。 使用 **“子报表属性”**对话框 -&amp;amp;gt;“参数”。|`[@Category]`<br /><br /> `[@Category]`|  
  
##  <a name="Complex"></a> 使用复杂表达式  
 复杂表达式可包含多个内置引用、运算符和函数调用，它在设计图面上显示为 `<<Expr>>`。 若要查看或更改表达式文本，则必须打开 **“表达式”** 对话框或在“属性”窗格中直接键入一个表达式。 下表列出了复杂表达式的常见用法，可用于显示或组织数据、更改报表外观（包括要设置的属性、通常用于设置该属性的对话框以及属性的值）。 可以在对话框、设计图面或“属性”窗格中直接键入表达式。  
  
|功能|属性、上下文和对话框|属性值|  
|-------------------|---------------------------------------|--------------------|  
|计算数据集的聚合值。|文本框中占位符的 Value 属性。 使用 **“占位符属性”**对话框 -&gt;“常规”。|`=First(Fields!Sales.Value,"DataSet1")`|  
|在同一文本框中串联文本和表达式。|位于页眉或页脚中的文本框中占位符的值。 使用 **“占位符属性”**对话框 -&gt;“常规”。|`="This report began processing at " & Globals!ExecutionTime`|  
|计算不同作用域中的数据集的聚合值。|位于 Tablix 组中的文本框中占位符的值。 使用 **“占位符属性”**对话框 -&gt;“常规”。|`=Max(Fields!Total.Value,"DataSet2)`|  
|根据值设置文本框中数据的格式。|Tablix 详细信息行中的文本框中占位符的颜色。 使用 **“文本框属性”**对话框 -&gt;“字体”。|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|计算一次要在整个报表中引用的值。|报表变量的值。 使用 **“报表属性”**对话框 -&gt;“变量”。|`=Variables!MyCalculation.Value`|  
|包含数据集中多个字段的特定值。|Tablix 中组的筛选器公式。 使用 **“Tablix 属性”**对话框 -&gt;“筛选器”。|对于数据类型，请选择 **Boolean**。<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|隐藏设计图面上的文本框，用户可使用名为 *Show*的布尔型参数切换该文本框。|文本框中的 Hidden 属性。 使用 **“文本框属性”**对话框 -&gt;“可见性”。|`=Not Parameters!`*显示\<布尔型参数 >*`.Value`|  
|指定动态页眉或页脚内容。|位于页眉或页脚中的文本框中占位符的值。|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|使用参数动态指定数据源。|数据源中的连接字符串。 使用 **“数据源属性”**对话框 -&gt;“常规”。|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|标识用户选定的多值参数的所有值。|文本框中占位符的值。 使用 **“Tablix 属性”**对话框 -&gt;“筛选器”。|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|为不含其他组的 Tablix 中的每 20 行指定一个分页符。|Tablix 中组的组表达式。 使用 **“组属性”**对话框 -&gt;“分页符”。 选择选项 **“在组的各实例之间”**。|`=Ceiling(RowNumber(Nothing)/20)`|  
|基于参数指定条件可见性。|Tablix 的 Hidden 属性。 使用 **“Tablix 属性”**对话框 ->“可见性”。|`=Not Parameters!<` *布尔参数* `>.Value`|  
|指定针对特定区域性而设置格式的日期。|数据区域中的文本框中占位符的值。 使用 **“文本框属性”**对话框 -&gt;“常规”。|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|将字符串与格式为两位小数的百分比的数字串联。|数据区域中的文本框中占位符的值。 使用 **“文本框属性”**对话框 -&amp;amp;gt;“常规”。|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [表达式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [报表参数 &#40;报表生成器和报表设计器 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [筛选器公式示例 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [筛选器、 组中，以及对数据进行排序和 #40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [页眉和页脚 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [格式设置文本和占位符 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [隐藏项 &#40;报表生成器和 SSRS &#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
