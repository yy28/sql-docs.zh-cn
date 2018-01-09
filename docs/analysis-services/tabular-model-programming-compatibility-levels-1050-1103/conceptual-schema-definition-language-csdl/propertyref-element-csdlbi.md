---
title: "PropertyRef 元素 (CSDLBI) |Microsoft 文档"
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
ms.assetid: 8299efb9-e224-4a82-bdfc-a74ec92f8711
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9df2f9bfd77a854c90f08ed8b4314bfa212bf469
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="propertyref-element-csdlbi"></a>PropertyRef 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]PropertyRef 元素是一个简单类型，提供对提供所需的另一个属性的值的列的引用。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 PropertyRef 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|“属性”|是|一个包含属性名称的字符串，该属性是引用的目标。|  
  
## <a name="propertyrefs-element"></a>PropertyRefs 元素  
 PropertyRefs 是一种复杂类型，用于定义 PropertyRef 元素中包含的每个属性的属性集合。  
  
 下表列出了 PropertyRefs 类型的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|是|一个包含属性引用的字符串。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示一个 PropertyRef 元素，该元素指定在 AdventureWorks 表格模型示例的某个度量值中使用的公式的源。  
  
```  
<bi:Measure Caption="Total Current Quarter Margin Performance" ReferenceName="Total Current Quarter Margin Performance" Width="0" IsSimpleMeasure="false">  
  <bi:Kpi StatusGraphic="Three Symbols UnCircled Colored">  
    <bi:KpiGoal>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Goal_" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Status_" />  
    </bi:KpiStatus>  
  </bi:Kpi>  
</bi:Measure>  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 Contoso Operations 多维数据集中的一个 KPI。 PropertyRef 元素指向若干列，这些列包含用于定义 KPI 相对于该目标的目标和状态的公式或值。  
  
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
  
  
