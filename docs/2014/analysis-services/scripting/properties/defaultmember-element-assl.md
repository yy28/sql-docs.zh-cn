---
title: DefaultMember 元素 (ASSL) |Microsoft 文档
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
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 71b8b2ecd1d5cd46ea50cceebe2a0105d9b7311f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026866"
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
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributePermission](../objects/attributepermission-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)， [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DefaultMember` 元素定义父元素的默认成员。 如果`DefaultMember`未指定或设置为空字符串， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]选择成员使用作为默认成员。  
  
 对于 `ManyToManyMeasureGroupDimension` 元素，`DefaultMember` 元素包含一个 MDX 表达式，该表达式指定在 `CubeDimensionID` 的 `ManyToManyMeasureGroupDimension` 元素中标识的维度的成员。 MDX 表达式是类似于[StrToMember](/sql/mdx/strtomember-mdx) MDX 函数使用受约束的关键字，在于它不能包含 MDX 或用户定义函数。  
  
 有关默认成员的详细信息，请参阅 [定义默认成员](../../multidimensional-models/attribute-properties-define-a-default-member.md)。  
  
 对应的父级的元素`DefaultMember`分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.AttributePermission>， <xref:Microsoft.AnalysisServices.DimensionAttribute>，和<xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
