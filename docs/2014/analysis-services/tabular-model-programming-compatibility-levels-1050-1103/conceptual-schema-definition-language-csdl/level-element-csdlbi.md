---
title: Level 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: fdf75c47-77dc-4bdb-9931-8eca198fdb88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b932ac5fac719be29bda37f134f9beb06d1483f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104777"
---
# <a name="level-element-csdlbi"></a>Level 元素 (CSDLBI)
  Level 元素是定义层次结构中的单个级别的复杂类型  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Level 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|数据源|用户帐户控制|属性引用的容器。|  
|PropertyRef|用户帐户控制|对实例属性的引用。 可以从所引用的实例属性中获取其他级别属性（例如标题、名称和引用名称）。 如果是这样，则不需要在 Level 元素中指定这些属性。|  
  
## <a name="remarks"></a>备注  
 有关表格模型中的层次结构的详细信息，请参阅[层次结构元素 (CSDLBI)](hierarchy-element-csdlbi.md)。  
  
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
  
## <a name="see-also"></a>请参阅  
 [了解表格对象模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [了解 DAX 中父子层次结构的函数](https://msdn.microsoft.com/library/gg492192(v=sql.120).aspx)   
 [配置&#40;所有&#41;属性层次结构的级别](../../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
