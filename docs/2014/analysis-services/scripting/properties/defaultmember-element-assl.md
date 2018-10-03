---
title: DefaultMember 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DefaultMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c90abe48fc1d3bfa099e39234d22df822a03782
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055289"
---
# <a name="defaultmember-element-assl"></a>DefaultMember 元素 (ASSL)
  包含标识父元素的默认成员的多维表达式 (MDX) 表达式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributePermission> <!-- or DimensionAttribute, ManyToManyMeasureGroupDimension, PerspectiveAttribute -->  
      ...  
   <DefaultMember>...</DefaultMember>  
      ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributePermission](../objects/attributepermission-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)， [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `DefaultMember` 元素定义父元素的默认成员。 如果`DefaultMember`未指定或为空字符串，设置[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]选择一个成员作为默认成员。  
  
 对于 `ManyToManyMeasureGroupDimension` 元素，`DefaultMember` 元素包含一个 MDX 表达式，该表达式指定在 `CubeDimensionID` 的 `ManyToManyMeasureGroupDimension` 元素中标识的维度的成员。 MDX 表达式是类似于[StrToMember](/sql/mdx/strtomember-mdx) MDX 函数含有 CONSTRAINED 关键字，因为它不能包含 MDX 函数或用户定义的函数。  
  
 有关默认成员的详细信息，请参阅 [定义默认成员](../../multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
 父级对应的元素`DefaultMember`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.AttributePermission>， <xref:Microsoft.AnalysisServices.DimensionAttribute>，和<xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
