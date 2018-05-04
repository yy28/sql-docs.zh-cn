---
title: Kpi |Microsoft 文档
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
ms.assetid: a0524602-5239-45a7-8c44-2477302a3637
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bb035968cc7c9b5bc40bf176907221becf29076d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="kpis"></a>KPI
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在表格模型中，KPI（关键绩效指标）用于根据目标值（由度量值或绝对值定义）度量某一值（由基础度量值定义）的性能。 本文提供了表格模型作者 Kpi 表格模型中一个基本的了解。  
  
##  <a name="bkmk_benefits"></a> 优点  
 在业务术语中，关键绩效指标 (KPI) 是一个用于度量业务目标的可计量度量值。 经常会在一段时间内评估 KPI。 例如，组织的销售部门可以使用 KPI 来根据预计的毛利润来度量每月毛利润。 会计部门可以度量每月的支出与收入之比以便评估成本，而人力资源部门可以度量每季度员工流失情况。 这两个都是 KPI 的示例。 业务专业人员经常使用以业务计分卡形式分组在一起的 KPI 获取迅速且精确的业务绩效历史摘要或标识趋势。  
  
 表格模型中的 KPI 包括：  
  
 **基础值**  
 基础值由解析为值的度量值定义。 例如，该值可以是实际销售额或计算出的度量值（例如给定期间的利润）的聚合。  
  
 **目标值**  
 目标值由解析为值的度量值定义，也可由绝对值定义。 例如，目标值可以是组织的业务经理希望增加的销售额或利润的数量。  
  
 **状态阈值**  
 状态阈值按下限和上限之间的范围或按固定值定义。 状态阈值在显示时含一个图形，可帮助用户轻松地确定与目标值相比基础值的状态。  
  
##  <a name="bkmk_example"></a> 示例  
 Adventure Works 的销售经理想要创建一个数据透视表，她可以使用该数据透视表快速显示销售人员是否满足针对给定期间（年）的销售定额。 对于每名销售人员，她希望该数据透视表显示以美元为单位的实际销售额、以美元为单位的销售定额以及一个简单的图形，该图形显示一个状态，指示每位销售人员是低于、等于还是高于其销售定额。 她希望能够按年对数据进行切片。  
  
 为此，该销售经理登记请求其组织的 BI 解决方案开发人员的帮助，以便将一个 Sales KPI 添加到 AdventureWorks 表格模型。 然后，该销售经理将使用 Excel 连接到 Adventure Works 表格模型作为数据源并创建数据透视表字段 （度量值和 KPI） 和切片器来分析销售人员达到其配额。  
  
 在模型中，将在 FactResellerSales 表中的 SalesAmount 列上创建一个度量值，该度量值提供以美元为单位的实际销售额。 该度量值定义该 KPI 的基础值。  
  
 将使用以下公式创建该 Sales 度量值：  
  
```  
Sales:=Sum(FactResellerSales[SalesAmount])  
```  
  
 FactSalesQuota 表中的 SalesAmountQuota 列具有为每位员工定义的销售定额。 该列中的值将充当 KPI 中的目标度量值（值）。  
  
 将使用以下公式创建该 SalesAmountQuota 度量值：  
  
```  
Target SalesAmountQuota:=Sum(FactSalesQuota[SalesAmountQuota])  
```  
  
> [!NOTE]  
>  在 FactSalesQuota 表的 EmployeeKey 列和 DimEmployees 表的 EmployeeKey 列之间存在一个关系。 该关系是必需的，以便 DimEmployee 表中的每位销售人员在 FactSalesQuota 表中体现出来。  
  
 在创建了度量值以便充当 KPI 的基础值和目标值后，对该 Sales 度量值进行扩展以便成为新的 Sales KPI。 在 Sales KPI 中，Target SalesAmountQuota 度量值定义为目标值。 “状态”阈值定义为某一百分比的范围，100% 的目标意味着 Sales 度量值定义的实际销售额满足在 Target SalesAmoutnQuota 度量值中定义的定额。 在状态栏上定义下限和上限百分比，并且选择图形类型。  
  
 该销售经理现在可以创建一个数据透视表，并且将该 KPI 的基础值、目标值和状态添加到“值”字段。 Employees 列将添加到 RowLabel 字段，而 CalendarYear 列作为切片器添加。  
  
 该销售经理可以按年对实际销售额、销售定额和每位销售员工的状态执行切片操作。 她可以分析多年中的销售趋势，以便确定是否需要调整某位销售人员的销售定额。  
  
##  <a name="bkmk_create"></a> Create and edit KPIs  
 为了在模型设计器中创建 KPI，您将使用“关键绩效指标”对话框。 因为 KPI 必须与某一度量值相关联，所以，您将通过以下方式创建 KPI：扩展求值结果为某一基础值的度量值，然后或者创建求值结果为目标值的度量值，或者输入绝对值。 在定义了基础度量值（值）和目标值之后，您可以定义基础值和目标值之间的状态阈值参数。 使用可选的图标、条、图形或颜色以图形格式显示该状态。 然后，可以将基础值和目标值以及状态以可以对其他数据字段执行切片操作的值的形式添加到报表或数据透视表中。  
  
 若要查看“关键绩效指标”对话框，请在表的度量值网格中，右键单击将充当基础值的度量值，然后单击 **“创建 KPI”**。 在某一度量值已作为基础值扩展到 KPI 后，一个图标将出现在度量值网格中的该度量值名称旁，以便将该度量值标识为与某一 KPI 相关联。  
  
##  <a name="bkmk_related_tasks"></a> 相关任务  
  
|主题|Description|  
|-----------|-----------------|  
|[创建和管理 KPI](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)|说明如何使用基础度量值、目标度量值和状态阈值创建 KPI。|  
  
## <a name="see-also"></a>另请参阅  
 [度量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [透视](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  
