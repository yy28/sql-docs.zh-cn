---
title: MemberRef 元素 (CSDLBI) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb0912afd99c7a4859ca4750a3ba1b66fdecd5f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205708"
---
# <a name="memberref-element-csdlbi"></a>MemberRef 元素 (CSDLBI)
  MemberRef 元素标识作为引用目标的属性的名称。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 MemberRef 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|“属性”|用户帐户控制|MemberRef 元素中包含的属性的名称。|  
  
## <a name="memberrefs-element"></a>MemberRefs 元素  
 MemberRefs 是一种复杂类型，用于定义 MemberRef 元素中包含每个成员的成员集合。  
  
 下表列出了 MemberRefs 类型的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|MemberRef|用户帐户控制|一个包含成员引用的字符串。|  
  
## <a name="example"></a>示例  
 **表格**  
  
 以下示例（在 CSDLBI 版本 1.1 中）表示 AdventureWorks 示例数据模型中定义 Products 表的部分。 此处，MemberRef 元素用于模型的默认字段集中包含的每一列。  
  
```  
  
<bi:EntityType>  
   <bi:DefaultDetails>  
     <bi:MemberRef Name="Color" />  
     <bi:MemberRef Name="DealerPrice" />  
     <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>示例  
 **多维**  
  
 以下示例（在 CSDLBI 版本 1.1 中）表示 Contoso Operations 多维数据集中定义 Bikes 表的部分。 在此示例中，MemberRef 元素用于指定一个列的名称（该列用作报表中的默认字段集），而另一个 MemberRef 元素用于引用提供排序顺序的列。  
  
```  
  
<bi:DefaultDetails>  
   <bi:MemberRef Name="Color" />  
</bi:DefaultDetails>  
  
<bi:SortMembers>  
   <bi:MemberRef Name="Color" />  
</bi:SortMembers>  
  
```  
  
## <a name="see-also"></a>请参阅  
 [用于商业智能的 CSDL 注释技术参考](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
