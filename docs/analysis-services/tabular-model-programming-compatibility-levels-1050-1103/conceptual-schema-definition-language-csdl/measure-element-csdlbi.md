---
title: 测量元素 (CSDLBI) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31bcb52bb9d1d0cf90b81ddc39ea838b00ece02f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="measure-element-csdlbi"></a>Measure 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Measure 元素是基于 CSDL 的 Property 元素的复杂类型。 CSDLBI 注释添加了一些属性，以支持要在商业智能数据模型中使用的复杂公式。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Measure 元素的元素和属性，以及适用于 Property 元素的所有属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|Kpi|“否”|仅对于用作 KPI 的度量值是必需元素。 并非所有度量值都是 KPI，但所有 KPI 都必须基于度量值的定义。<br /><br /> [KPI 元素 & #40;CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)|  
|IsSimpleMeasure|“否”|一个 true/false 值，指示度量值中使用的公式是否为简单聚合（SUM、COUNT、MIN、MAX、AVG、DistinctCount）之一。<br /><br /> 默认为 true。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 AdventureWorks 表格模型示例中的度量值。 已通过添加 KPI 元素将第二个度量值转换为 KPI。  
  
```  
  
<Property   
    Name="Order_Lines_Count"   
    Type="Int64">  
<bi:Measure   
    Caption="Order Lines Count"   
    ReferenceName="Order Lines Count"   
    Width="0"   
    IsSimpleMeasure="false" />  
</Property>  
  
<Property   
    Name="Total_Current_Quarter_Sales_Performance"   
    Type="Double">  
<bi:Measure   
    Caption="Total Current Quarter Sales Performance"   
    ReferenceName="Total Current Quarter Sales Performance"   
    Width="0"   
    IsSimpleMeasure="false">  
    <bi:Kpi   
    StatusGraphic="Three Signs Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Goal_" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Status_" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
```  
  
## <a name="example"></a>示例  
 **Multidimensiona;**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 Contoso Operations 多维数据集中一个正用作 KPI 的度量值。  
  
```  
  
<Property   
    Name="Sum_of_SalesAmount"   
    Type="Decimal" Precision="19" Scale="4">  
<Documentation>  
<Summary>KPI Description</Summary>  
</Documentation>  
<bi:Measure   
    Caption="Sum of SalesAmount"   
    ReferenceName="Sum of SalesAmount"   
    FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
<bi:Kpi   
    StatusGraphic="Three Circles Colored">  
    <bi:KpiGoal>  
        <bi:PropertyRef Name="v_Sum_of_SalesAmount_Goal" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
        <bi:PropertyRef Name="v_Sum_of_SalesAmount_Status" />  
    </bi:KpiStatus>  
</bi:Kpi>  
</bi:Measure>  
</Property>  
```  
  
## <a name="see-also"></a>另请参阅  
 [BI 批注的 CSDL 的技术参考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
