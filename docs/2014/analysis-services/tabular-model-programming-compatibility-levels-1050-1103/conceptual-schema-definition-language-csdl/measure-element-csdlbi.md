---
title: 度量值元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: bfbc9274-053a-421a-bb81-2095bba710be
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de02e5c0233fb5cb1699f038b87871c8757f0256
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068397"
---
# <a name="measure-element-csdlbi"></a>Measure 元素 (CSDLBI)
  Measure 元素是基于 CSDL 的 Property 元素的复杂类型。 CSDLBI 注释添加了一些属性，以支持要在商业智能数据模型中使用的复杂公式。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Measure 元素的元素和属性，以及适用于 Property 元素的所有属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|Kpi|否|仅对于用作 KPI 的度量值是必需元素。 并非所有度量值都是 KPI，但所有 KPI 都必须基于度量值的定义。<br /><br /> [KPI 元素&#40;CSDLBI&#41;](kpi-element-csdlbi.md)|  
|IsSimpleMeasure|否|一个 true/false 值，指示度量值中使用的公式是否为简单聚合（SUM、COUNT、MIN、MAX、AVG、DistinctCount）之一。<br /><br /> 默认为 true。|  
  
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
  
## <a name="see-also"></a>请参阅  
 [用于商业智能的 CSDL 注释技术参考](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
