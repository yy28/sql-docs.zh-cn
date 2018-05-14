---
title: KpiGoal 元素 (CSDLBI) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb6da0218ec4261f57fe15b77c3e5040ca62f3c2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="kpigoal-element-csdlbi"></a>KpiGoal 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  KpiGoal 元素提供对某列的引用，而该列用于定义关键绩效指标 (KPI) 的目标。  
  
 在 CSDLBI 中，KPI 基于度量值，Measure 元素包含公式（如果有），而与 KPI 关联的其他元数据被定义为此 [KPI 元素 (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md) 的一部分。  Kpigoal 元素是 Kpi 元素的子类型。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 KpiGoal 元素的元素和属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|是|对包含 KPI 目标值的列的引用。<br /><br /> Kpigoal 元素必须只包含一个 PropertyRef 元素。<br /><br /> 请参阅 [PropertyRef 元素 (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 AdventureWorks 示例模型中的一个 KPI。  
  
```  
  
<Property Name="InternetCurrentSalesPerformance" Type="Double">  
  <bi:Measure>  
    <bi:Kpi StatusGraphic="Three Stars Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Goal" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Status" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 Contoso Operations 多维数据集中的一个 KPI。  
  
```  
<bi:Measure   
       Caption="Sum of SalesAmount"   
       ReferenceName="Sum of SalesAmount"   
       FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
    <bi:Kpi   
       StatusGraphic="Three Circles Colored">  
      <bi:KpiGoal>  
         <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Goal" />  
       </bi:KpiGoal>  
       <bi:KpiStatus>  
          <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Status" />  
        </bi:KpiStatus>  
       </bi:Kpi>  
</bi:Measure>  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [KPI 元素 & #40;CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
  
