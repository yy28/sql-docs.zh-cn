---
title: KpiStatus 元素 (CSDLBI) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6fee5b82-caa8-46a1-ad68-bbce3e11e01e
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 003dd6f1458266b4f58b1445fc70e2030d0f0ea6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015767"
---
# <a name="kpistatus-element-csdlbi"></a>KpiStatus 元素 (CSDLBI)
  KpiStatus 元素定义对某列的引用，该列包含用作关键绩效指标 (KPI) 中的状态指示器的值。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 KpiStatus 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|是|对某列的引用，该列包含用作 KPI 中的状态指示器的值。<br /><br /> 此元素必须正好包含一个列引用，如 TPropertyRefcomplex 类型所定义。|  
  
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
  
  