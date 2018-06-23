---
title: KPI 元素 (CSDLBI) |Microsoft 文档
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
ms.assetid: 203ee6e8-eef2-4476-b09f-bd95e492ddaa
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 2f6c4ee26beb74acd6817615d34847883c3b3565
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129760"
---
# <a name="kpi-element-csdlbi"></a>KPI 元素 (CSDLBI)
  Kpi 元素定义一个可用作关键绩效指标 (KPI) 的计算。 在商业智能数据模型中，KPI 基于度量值，因此，KPI 的定义包含与度量值关联的所有元数据以及展示 KPI 值所需的信息，包括默认图形。  
  
 Kpi 元素不指定包含在度量值定义中的公式，而是指定与用作 KPI 的度量值关联的其他元数据。 一旦您将度量值指定为 KPI，就无法在其他上下文中将其用作度量值。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Kpi 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|文档|“否”|KPI 的说明。|  
|KpiGoal|是|对列的引用，该列包含可用作目标的值。<br /><br /> 请参阅 [PropertyRef 元素 (CSDLBI)](propertyref-element-csdlbi.md)。|  
|KpiStatus|是|对列的引用，该列包含表示 KPI 的当前状态的值。|  
|StatusGraphic|是|对于一幅图像的引用，此图像指示针对在 KPI 中定义的目标，进度为负、零还是正。|  
  
## <a name="remarks"></a>Remarks  
 当您设计模型时，您可以通过创建度量值，然后指定将度量值用作 KPI，以创建 KPI。 然后，添加特定于 KPI 的信息，如在显示趋势时使用的图形。  
  
## <a name="example"></a>示例  
 **表格**  
  
 下面的示例（在 CSDLBI 版本 1.0 中）显示 AdventureWorks 表格模型示例中度量销售额的 KPI。  
  
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
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 Contoso Operations 多维数据集中的一个 KPI。  
  
```  
<Property Name="Sum_of_SalesAmount" Type="Decimal" Precision="19" Scale="4">  
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
  
  