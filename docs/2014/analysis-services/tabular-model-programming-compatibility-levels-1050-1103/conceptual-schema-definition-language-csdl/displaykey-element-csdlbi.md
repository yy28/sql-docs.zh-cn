---
title: DisplayKey 元素 (CSDLBI) |Microsoft 文档
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
ms.assetid: 7d881278-1e77-42e1-8cfc-f1bbd9ec2340
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 907bb04d59225180fad91b63971d578181c6663d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027532"
---
# <a name="displaykey-element-csdlbi"></a>DisplayKey 元素 (CSDLBI)
  DisplayKey 元素包含共同构成强标识符的以下元素的列表。 DisplayKey 只作为 EntityType 元素的子项存在。 它可以引用列或角色方。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了 DisplayKey 元素的属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|IsDisplayKey|“否”|True 或 False。|  
  
## <a name="remarks"></a>Remarks  
 此元素不用于报表。 您将此属性应用到的元素不需要是实际的表键，而只是一个您将显示为键的元素。 但是，您用于 DisplayKey 的列必须包含唯一值。  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示 AdventureWorks 示例数据模型中的一列，该列已被指定为表的 DisplayKey。  
  
```  
<sample in progress>  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示了来自 Contoso Operations 多维数据集的表示形式的摘录。 在这一模型中，Color 列已标记为 Bikes 表的显示键。  
  
```  
  
<EntityType   
    Name="Bike">  
.. .. ..  
<Property   
    Name="Color"   
    Type="String"   
    MaxLength="Max"   
    Unicode="true"   
    FixedLength="false">  
<bi:Property   
    ContextualNameRule="Context"   
    Alignment="Left" Units="counts"   
    SortDirection="Descending"   
    IsRightToLeft="true"   
    DefaultAggregateFunction="Max" />  
</Property>  
.. .. ..  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>>  
.. .. ..  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>请参阅  
 [了解表格对象模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 概念](../csdlbi-concepts.md)  
  
  