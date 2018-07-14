---
title: Hierarchy 元素 (CSDLBI) |Microsoft Docs
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
ms.assetid: 9debb638-1b28-401b-9499-8f63943863e9
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be67c3059f09beefae68d0264fd0316579344d64
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250787"
---
# <a name="hierarchy-element-csdlbi"></a>Hierarchy 元素 (CSDLBI)
  Hierarchy 元素是表中可彼此链接以形成层次结构的各个字段的逻辑容器。 Hierarchy 元素派生自 CSDL 的 Member 元素，并已扩展为支持在商业智能数据模型中创建的层次结构。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Hierarchy 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|文档|“否”|层次结构的说明。|  
|级别|是|定义层次结构中使用的列的一个或多个 Level 元素。<br /><br /> 请参阅 [Level 元素 (CSDLBI)](level-element-csdlbi.md)。|  
  
## <a name="remarks"></a>Remarks  
 在表格模型中，层次结构是通过在同一个表的各列间指定父子关系来创建的。 有关详细信息，请参阅[层次结构（SSAS 表格）](../../tabular-models/hierarchies-ssas-tabular.md)。  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下示例（在 CSDLBI 版本 1.0 中）显示了 AdventureWorks 示例模型中已添加到 Products 表的一个层次结构。  
  
```  
  
<bi:Hierarchy Name="Categoryy">  
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
  
 下面的示例（在 CSDLBI 版本 1.1 中）显示 Contoso Retail Operations 多维数据集中的一个层次结构。  
  
```  
  
<bi:Hierarchy Name="Product_Hierarchy" Caption="Product Hierarchy" ReferenceName="Product Hierarchy">  
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
  
  
