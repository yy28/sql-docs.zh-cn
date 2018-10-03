---
title: KpiGoal 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: fd8afbe7-b57d-4b47-862d-eb7b2489c327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ceee819fb887e2a45b3f366b261fba00df4776a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191377"
---
# <a name="kpigoal-element-csdlbi"></a>KpiGoal 元素 (CSDLBI)
  KpiGoal 元素提供对某列的引用，而该列用于定义关键绩效指标 (KPI) 的目标。  
  
 在 CSDLBI 中，KPI 基于度量值，Measure 元素包含公式（如果有），而与 KPI 关联的其他元数据被定义为此 [KPI 元素 (CSDLBI)](kpi-element-csdlbi.md) 的一部分。  Kpigoal 元素是 Kpi 元素的子类型。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 KpiGoal 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|用户帐户控制|对包含 KPI 目标值的列的引用。<br /><br /> Kpigoal 元素必须只包含一个 PropertyRef 元素。<br /><br /> 请参阅 [PropertyRef 元素 (CSDLBI)](propertyref-element-csdlbi.md)。|  
  
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
  
## <a name="see-also"></a>请参阅  
 [KPI 元素&#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
  
