---
title: 其 RootMemberIf 元素 (ASSL) |Microsoft 文档
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
- RootMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a923b08efc636d2635d60b00f85c42dc00a312e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018708"
---
# <a name="rootmemberif-element-assl"></a>RootMemberIf 元素 (ASSL)
  确定如何识别父级属性的根成员或成员。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <RootMemberIf>...</RootMemberIf>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*ParentIsBlankSelfOrMissing*|  
|基数|0-1：可出现一次且仅出现一次的可选元素|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值`RootMemberIf`元素仅由父属性 (换而言之，值[用法](usage-element-dimensionattribute-assl.md)元素`DimensionAttribute`父元素设置为*父*) 来确定根 （父-子层次结构的最顶层） 成员。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|只有符合一个或多个所述的条件的成员*ParentIsBlank*， *ParentIsSelf*，或*ParentIsMissing*会被视为根成员。|  
|*ParentIsBlank*|仅具有 null 值、 零或空字符串所表示的键列中的成员[KeyColumns](../collections/columns-element-assl.md)集合`DimensionAttribute`会被视为根成员。|  
|*ParentIsSelf*|只有本身作为父级的成员才会被视为根成员。|  
|*ParentIsMissing*|只有无法找到其父级的成员才会被视为根成员。|  
  
 对应于的允许值为枚举`RootMemberIf`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.RootIfValue>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  