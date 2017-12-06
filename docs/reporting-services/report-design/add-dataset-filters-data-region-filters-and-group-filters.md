---
title: "添加数据集筛选器、数据区域筛选器和组筛选器| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fcca7243-a702-4725-8e6f-cf118e988acf
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: ead354a4f95b061f44728b76bbbccd6ef84606a0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="add-dataset-filters-data-region-filters-and-group-filters"></a>添加数据集筛选器、数据区域筛选器和组筛选器
  在报表中，筛选器是创建的数据集、数据区域或数据区域组的一部分，用于限制报表中使用的数据。 如果无法更改数据集查询（例如，如果您使用的是共享数据集），则可使用筛选器帮助您控制报表数据。  
  
 筛选器可帮助您控制在报表中显示和处理的数据。 可以为数据集、数据区域或组的任意组合指定筛选器。  
  
 有关详细信息，请参阅[向数据集添加筛选器（报表生成器和 SSRS）](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)和[筛选器公式示例（报表生成器和 SSRS）](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="When"></a> 选择设置筛选器的时间  
 无法在数据源中筛选数据时，请为报表项指定筛选器。 例如，当数据源不支持查询参数、您必须运行存储过程且无法修改查询或者参数化报表快照显示不同用户的自定义数据时，请使用报表筛选器。  
  
 在检索报表数据集之前或之后都可以对该报表数据进行筛选。 若要在检索之前筛选数据，请更改每个数据集的查询。 筛选查询中的数据时，可在数据源中筛选数据，这样可以减少必须在报表中检索和处理的数据量。 若要在检索之后筛选数据，请在报表中创建筛选表达式。 可以为数据集、数据区域或组（包括详细信息组）设置筛选表达式。 还可以在筛选表达式中包含参数，从而提供一种为特定值或特定用户筛选数据的方式。例如，对标识查看报表的用户的值进行筛选。  
  
##  <a name="Where"></a> 选择设置筛选器的位置  
 筛选器的设置位置应根据您希望在报表中获得的效果来确定。 在运行时，报表处理器按以下顺序应用筛选器：先对数据集，再对数据区域，最后对组，在每个组层次结构中按自上而下的顺序。 在表、矩阵或列表中，对行组、列组和相邻组分别应用各自的筛选器。 在图表中，对类别组和序列组分别应用各自的筛选器。 报表处理器应用筛选器时，会按每个报表项 **“属性”** 对话框的 **“筛选器”** 页上定义的顺序应用所有筛选器公式，这等效于使用布尔 AND 操作组合所有筛选器公式。  
  
 下面的列表比较对不同报表项设置筛选器的效果：  
  
-   **对数据集** ：如果希望以相同方式筛选绑定到单个数据集的一个或多个数据区域，则可对数据集设置筛选器。 例如，对同时绑定到显示销售数据的表和显示同一数据的图表的数据集设置筛选器。  
  
-   **对数据区域** ：如果希望绑定到单个数据集的一个或多个数据区域提供该数据集的不同视图，则可对数据区域设置筛选器。 例如，对一个表数据区域设置筛选器以显示销售额排在前十名的商店，对另一个表数据区域设置筛选器以显示同一报表中销售额排在末十名的商店。  
  
-   **对 Tablix 数据区域中的行组或列组** ：如果希望组表达式包含或排除某些值以控制表、矩阵或列表中出现的组值，则可对组设置筛选器。  
  
-   **对 Tablix 数据区域中的详细信息组** ：如果一个数据区域中有多个详细信息组并且您希望每个详细信息组显示数据集中不同的一组数据，则可对详细信息组设置筛选器。  
  
-   **对图表数据区域中的序列组或类别组** ：如果希望组表达式包含或排除某些值以控制图表中出现的值，则可对序列组或类别组设置筛选器。  
  
 返回页首  
  
##  <a name="FilterEquations"></a> 了解筛选器公式  
 在运行时，报表处理器会将值转换为指定数据类型，然后使用指定运算符来比较表达式和值。 下面列出筛选器公式的每个部分：  
  
-   **表达式** ：定义对其进行筛选的内容。 通常为数据集字段。  
  
-   **数据类型** ：指定在运行时报表处理器计算筛选器公式时所用的数据类型。 您所选择的数据类型必须是报表定义架构支持的数据类型之一。  
  
-   **运算符** ：定义如何比较筛选器公式的两个部分。  
  
-   **值** ：定义要在比较中使用的表达式。  
  
 以下部分介绍筛选器公式的每个部分。  
  
### <a name="expression"></a>表达式  
 当运行时报表处理器计算筛选器公式时，表达式和值的数据类型必须相同。 为 **“表达式”** 所选的字段的数据类型由从数据源检索数据时所用的数据处理扩展插件或数据访问接口确定。 为 **“值”** 输入的表达式的数据类型由 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 默认值确定。 所选数据类型由报表定义支持的数据类型确定。 来自数据库的值可能由数据访问接口转换为 CLR 类型。  
  
### <a name="data-type"></a>数据类型  
 为使报表处理器能比较两个值，值的数据类型必须相同。 下表列出了 CLR 数据类型和报表定义数据类型之间的映射。 从数据源中检索的数据可能转换为与作为报表数据时不同的数据类型。  
  
|**报表定义架构数据类型**|**CLR 类型**|  
|--------------------------------------------|-----------------------|  
|**Boolean**|**Boolean**|  
|**DateTime**|**DateTime**、 **DateTimeOffset**|  
|**Integer**|**Int16**、 **Int32**、 **UInt16**、 **Byte**、 **SByte**|  
|**Float**|**Single**、 **Double**、 **Decimal**|  
|**Text**|**String**、 **Char**、 **GUID**、 **Timespan**|  
  
 必须指定数据类型时，你可以在表达式的 Value 部分指定你自己的转换。  
  
### <a name="operator"></a>运算符  
 下表列出了可在筛选器公式中使用的运算符，以及报表处理器用于计算筛选器公式的内容。  
  
|运算符|操作|  
|--------------|------------|  
|**Equal、Like、NotEqual、GreaterThan、GreaterThanOrEqual、LessThan、LessThanOrEqual**|将表达式与一个值进行比较。|  
|**TopN、BottomN**|将表达式与一个 **Integer** 值进行比较。|  
|**TopPercent、BottomPercent**|将表达式与一个 **Integer** 或 **Float** 值进行比较。|  
|**Between**|测试表达式是否在两个值之间（含这两个值）。|  
|**In**|测试表达式是否包含在一组值中。|  
  
### <a name="value"></a>值  
 Value 表达式指定筛选器公式的最后一部分。 报表处理器会将计算后的表达式转换为指定的数据类型，然后计算整个筛选器公式以确定表达式中指定的数据是否通过了筛选器的筛选。  
  
 若要转换为非标准 CLR 数据类型的数据类型，必须修改表达式以显式转换为该数据类型。 您可使用 **“表达式”** 对话框的 **“常见函数”**下的 **“转换”**中列出的转换函数。 例如，对于 `ListPrice` 字段，该字段表示 **数据源中以** money [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型存储的数据，数据处理扩展插件将以 <xref:System.Decimal> 数据类型返回该字段值。 若要将筛选器设置为仅使用报表货币中大于 **$50000.00** 的值，则可使用表达式 `=CDec(50000.00)`将该值转换为 Decimal 类型。  
  
 此值还可以包括参数引用，以允许用户以交互方式选择作为筛选依据的值。  
  
 返回页首  
  
## <a name="see-also"></a>另请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
