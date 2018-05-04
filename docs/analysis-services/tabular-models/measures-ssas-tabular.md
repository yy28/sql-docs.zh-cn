---
title: 度量值 |Microsoft 文档
ms.custom: ''
ms.date: 04/10/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 27ec8f99-e9ef-44c9-a83f-f7c88e128ad3
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0b994ddc834317db4c0cb10c55ccd8ef33441473
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="measures"></a>度量值组
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在表格模型中，度量值是使用 DAX 公式创建的计算，以便用于报表客户端中。 系统根据用户在报告客户端应用程序中选择的字段、筛选器和切片器来计算度量值。  
  
##  <a name="bkmk_understanding"></a> 优点  
 度量值可以基于标准聚合函数，如 AVERAGE、COUNT 或 SUM；或者，您可以使用 DAX 定义自己的公式。 除了公式之外，每个度量值都具有属性（由度量值数据类型定义），如“名称”、“表详细信息”、“格式”和“小数位数”。  
  
 在模型中定义度量值后，用户可以将它们添加到报表或数据透视表。 根据透视和角色，度量值将与其关联表一起显示在字段列表中，可供模型的所有用户使用。 度量值通常在事实表中创建，但是可以独立于与之关联的表。  
  
 了解计算列和度量值之间的主要区别很重要。 在计算列中，公式为列中的每一行计算值。 例如，在 FactSales 表中，包含以下公式、名为 TotalProfit 的计算列为每一行计算总利润的值（每个销售对应一行）：  
  
```  
=[SalesAmount] - [TotalCost] - [ReturnAmount]  
```  
  
 然后可以在报告客户端中使用 TotalProfit 计算列，就像使用其他任意列一样。  
  
 另一方面，度量值则基于用户所做的选择（数据透视表或报告中设置的筛选上下文）计算值。 例如，使用以下公式在 FactSales 表中创建一个度量值：  
  
```  
Sum of TotalProfit: =SUM([TotalProfit])  
```  
  
 使用 Excel 的销售分析人员想知道每个产品类别的总利润。 每个产品类别包括多个产品。 销售分析人员选择 ProductCategoryName 列并将它添加到数据透视表的“行标签”筛选器窗口；然后对应每个产品类别的行将显示在数据透视表中。 用户然后选择 Sum of TotalProfit 度量值。 默认情况下，将度量值添加到“值”筛选器窗口。 该度量值为每个产品类别计算总利润之和并显示结果。 销售分析人员然后可以使用切片器进一步筛选每个产品类别的总利润之和，例如，添加 CalendarYear 作为切片器以按年查看每个产品类别的总利润之和。  
  
|ProductCategoryName|Sum of TotalProfit|  
|-------------------------|------------------------|  
|Audio|$2,731,061,308.69|  
|Cameras and Camcorders|$620,623,675.75|  
|Computers|$392,999,044.59|  
|Tv and Video|$946,989,702.51|  
|**总计**|**$4,691,673,731.53**|  
  
##  <a name="bkmk_def_mg"></a> Defining measures by using the measure grid  
 通过使用模型设计器中的度量值网格在设计时创建度量值。 每个表各有一个度量值网格。 默认情况下，度量值网格在模型设计器中显示在每个表的下方。 也可以选择不查看度量值网格来查找特定表。 若要切换表的度量值网格显示，请单击 **“表”** 菜单，然后单击 **“显示度量值网格”**。  
  
 在度量值网格中，您可以通过以下方式创建度量值：  
  
-   在度量值网格中单击空单元，然后在编辑栏中键入 DAX 公式。 单击 Enter 填写公式时，该度量值将显示在度量值网格的单元中。  
  
-   使用标准聚合函数创建度量值，方法是单击某列，单击工具栏上的“自动求和”按钮 (∑)，然后单击一个标准聚合函数。 标准聚合函数包括：Sum、Average、Count、DistinctCount、Max 和 Min。 使用“自动求和”按钮创建的度量值将始终显示在该列之下的度量值网格中。  
  
 默认情况下，使用“自动求和”时，按以下方式定义度量值的名称：相关列的名称后跟冒号和公式。 可以在编辑栏中更改该名称，也可以在“属性”窗口的 **“度量值名称”** 属性设置中更改它。 使用自定义公式创建度量值时，您可以在编辑栏中键入名称后跟冒号和公式，或者在“属性”窗口的 **“度量值名称”** 属性设置中键入名称。  
  
 它仔细是重要命名度量值。 度量值名称将随关联的表一起显示在报告客户端的字段列表中。 还将根据基础度量值命名 KPI。 度量值的名称不能与模型中任何表中的任何列的名称相同。  
  
> [!TIP]  
>  可将多个表中的度量值组合到一个表中（通过创建一个空表，然后将多个表中的度量值移入该表中），也可以在表中创建新的度量值。 请记住，您在引用其他表中的列时可能需要在 DAX 公式中包含表名称。  
  
 如果为模型定义了透视，不会自动将度量值添加到这些透视中。 您必须使用“透视”对话框手动将度量值添加到透视。 若要了解详细信息，请参阅[透视](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)。  
  
##  <a name="bkmk_properties"></a> 度量值属性  
 每个度量值具有定义它的属性。 可以在“属性”窗口中编辑度量值属性以及关联的列属性。 度量值具有以下属性：  
  
|属性|默认设置|Description|  
|--------------|---------------------|-----------------|  
|**Description**|空白|度量值的说明。 该说明将不与度量值一起显示在报告客户端中。|  
|**格式**|从公式表达式中引用的列的数据类型自动确定。|度量值的格式。 例如，货币或百分比。|  
|**公式**|创建度量值时在编辑栏中输入的公式。|度量值的公式。|  
|**“度量值名称”**|使用“自动求和”时，度量值名称将位于后跟冒号的列名之前。 如果输入自定义公式，请键入名称并且后跟冒号，然后键入该公式。|显示在报告客户端的字段列表中的度量值名称。|  
  
##  <a name="bkmk_KPI"></a> 在 KPI 中使用度量值  
 KPI（关键绩效指标）由“基础”值（由度量值定义）定义，用于与“目标”值（也由度量值或绝对值定义）进行对比。 KPI 还包括以图形格式显示的“状态” ，这是一种计算，其中会根据各阈值之间的目标值对基础值进行评估。 业务专业人员通常使用 KPI 来确定关键业务度量的趋势。  
  
 任何度量值都可以作为 KPI 的基础度量值。 若要创建 KPI，请在度量值网格中右键单击某度量值，然后单击“创建 KPI”。 将显示“关键绩效指标”对话框，您可以在此指定目标值（由度量值或绝对值定义）、定义状态阈值和图形类型。 若要了解详细信息，请参阅[Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)。  
  
##  <a name="bkmk_rel_tasks"></a> Related tasks  
  
|主题|Description|  
|-----------|-----------------|  
|[创建和管理度量值](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)|说明如何使用模型设计器中的度量值网格创建和管理度量值。|  
  
## <a name="see-also"></a>另请参阅  
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [创建和管理 Kpi](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)   
 [计算列](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
