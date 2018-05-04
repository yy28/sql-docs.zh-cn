---
title: MemberRef 元素 (CSDLBI) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 931bf8a2ee5d4cfd419a37f6fa5eae2de24cb64c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
  
  
