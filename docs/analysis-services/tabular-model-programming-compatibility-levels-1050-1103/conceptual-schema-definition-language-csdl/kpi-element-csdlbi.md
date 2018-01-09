---
title: "KPI 元素 (CSDLBI) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 203ee6e8-eef2-4476-b09f-bd95e492ddaa
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 28f4f65bc65ac1a5d231717ddbc552e83ef302de
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="kpi-element-csdlbi"></a>KPI 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Kpi 元素定义可用来为关键绩效指标 (KPI) 计算。 在商业智能数据模型中，KPI 基于度量值，因此，KPI 的定义包含与度量值关联的所有元数据以及展示 KPI 值所需的信息，包括默认图形。  
  
 Kpi 元素不指定包含在度量值定义中的公式，而是指定与用作 KPI 的度量值关联的其他元数据。 一旦您将度量值指定为 KPI，就无法在其他上下文中将其用作度量值。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Kpi 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|文档|是|KPI 的说明。|  
|KpiGoal|是|对列的引用，该列包含可用作目标的值。<br /><br /> 请参阅 [PropertyRef 元素 (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)。|  
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
  
## <a name="see-also"></a>另请参阅  
 [用于商业智能的 CSDL 注释技术参考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
