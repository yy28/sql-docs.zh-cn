---
title: DefaultDetails 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 05a08baa-23cc-4011-9c2e-f60a20bb87da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa1fcc05363cf356d5895c0d5e6f62c037f45fb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120857"
---
# <a name="defaultdetails-element-csdlbi"></a>DefaultDetails 元素 (CSDLBI)
  DefaultDetails 元素表示一系列属性参考，这些属性参考一起定义表中各列的“默认字段集”。 每个属性只能引用一个度量值或一列。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 DefaultDetails 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|DefaultDetailsPosition|否|指示在集合中存在与位置的正整数。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示了来自 AdventureWorks 示例数据模型的摘录。 对于 Employees 表 (Title) 只有一个默认列集。 但是，三个列已定义为 Products 表的默认字段集。  
  
```  
  
<EntityType   
    Name="DimEmployee">  
....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Title" />  
   </bi:DefaultDetails>  
.....  
<EntityType   
    Name="Products">  
.....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
      <bi:MemberRef Name="DealerPrice" />  
      <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下示例（在 CSDLBI 版本 1.1 中）显示了来自 Contoso Operations 多维数据集中 Bike 表定义的摘录。 此批注指示，如果未指定其他显示列，则应显示 Color 列。  
  
```  
  
<EntityType Name="Bike">  
   <Key>  
   <PropertyRef Name="RowNumber" />  
   </Key>  
....  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
   </bi:DefaultDetails>  
   <bi:SortMembers>  
      <bi:MemberRef Name="Color" />  
   </bi:SortMembers>  
....  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>请参阅  
 [了解表格对象模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 概念](../csdlbi-concepts.md)  
  
  
