---
title: "级别元素 (CSDLBI) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: fdf75c47-77dc-4bdb-9931-8eca198fdb88
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6d2896a01a8efeacb42bde203ad93e0efdb52be4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="level-element-csdlbi"></a>Level 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]级别元素为复杂类型定义的层次结构中的单个级别  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Level 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|数据源|是|属性引用的容器。|  
|PropertyRef|是|对实例属性的引用。 可以从所引用的实例属性中获取其他级别属性（例如标题、名称和引用名称）。 如果是这样，则不需要在 Level 元素中指定这些属性。|  
  
## <a name="remarks"></a>Remarks  
 有关表格模型中的层次结构的详细信息，请参阅[层次结构元素 (CSDLBI)](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md)。  
  
## <a name="example"></a>示例  
 **表格**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 AdventureWorks 表格模型示例中的某个层次结构内多个级别的定义。  
  
```  
  
<bi:Hierarchy Name="Category">  
   <bi:Level Name="CategoryName">  
     <bi:Source>  
       <bi:PropertyRef Name="CategoryName" />  
     </bi:Source>  
   </bi:Level>  
   <bi:Level Name="ProductName">  
     <bi:Source>  
       <bi:PropertyRef Name="ProductName" />  
     </bi:Source>  
   </bi:Level>  
</bi:Hierarchy>  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 Contoso Operations 多维数据集中一个具有多个级别的层次结构。  
  
```  
<bi:Hierarchy   
   Name="Product_Hierarchy"   
   Caption="Product Hierarchy"   
   ReferenceName="Product Hierarchy">  
     <bi:Documentation>  
        <bi:Summary>DESCRIPTION_ProductModelCateg_Hierarchies</bi:Summary>  
     </bi:Documentation>  
  
     <bi:Level Name="ProductLine">  
        <bi:Source>  
        <bi:PropertyRef Name="ProductLine" />  
        </bi:Source>  
     </bi:Level>  
  
     <bi:Level Name="ModelName">  
        <bi:Source>  
        <bi:PropertyRef Name="ModelName" />  
        </bi:Source>  
     </bi:Level>  
</bi:Hierarchy>  
```  
  
## <a name="see-also"></a>另请参阅  
 [了解表格对象模型在兼容性级别 1050年通过 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [了解 DAX 中的父-子层次结构函数](http://msdn.microsoft.com/en-us/b11f0cff-cee4-4ae7-a5b3-ebe288fc42d3)   
 [配置 &#40;所有 &#41;属性层次结构的级别](../../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
