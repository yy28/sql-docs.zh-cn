---
title: KpiStatus 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 6fee5b82-caa8-46a1-ad68-bbce3e11e01e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab554d47678b336ebfa763a7f3bd05f027e92945
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164537"
---
# <a name="kpistatus-element-csdlbi"></a>KpiStatus 元素 (CSDLBI)
  KpiStatus 元素定义对某列的引用，该列包含用作关键绩效指标 (KPI) 中的状态指示器的值。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 KpiStatus 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|用户帐户控制|对某列的引用，该列包含用作 KPI 中的状态指示器的值。<br /><br /> 此元素必须正好包含一个列引用，如 TPropertyRefcomplex 类型所定义。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 AdventureWorks 表格模型示例中的一个 KPI。 KpiStatus 元素引用包含该值的一列（表示为 PropertyRef）。  
  
```  
  
<Property Name="InternetCurrSalesPerf" Type="Double">  
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
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 Contoso Operations 多维数据集中的一个 KPI。 KpiStatus 元素引用一个度量值，该度量值计算 KPI 状态的值。  
  
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
  
  
