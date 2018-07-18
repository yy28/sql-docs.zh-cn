---
title: MemberRef 元素 (CSDLBI) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 79b6f2684dabcb45cfddac626bc2a6aa140298f3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039233"
---
# <a name="memberref-element-csdlbi"></a>MemberRef 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MemberRef 元素标识作为引用目标的属性的名称。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 MemberRef 元素的元素和属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|名称|是|MemberRef 元素中包含的属性的名称。|  
  
## <a name="memberrefs-element"></a>MemberRefs 元素  
 MemberRefs 是一种复杂类型，用于定义 MemberRef 元素中包含每个成员的成员集合。  
  
 下表列出了 MemberRefs 类型的元素和属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|MemberRef|是|一个包含成员引用的字符串。|  
  
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
  
## <a name="see-also"></a>另请参阅  
 [BI 批注的 CSDL 的技术参考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
