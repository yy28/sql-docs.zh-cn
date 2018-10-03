---
title: RootMemberIf 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fb10d62b14c5f13fbc26de23d832d77b724bebc6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118697"
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
|子元素|None|  
  
## <a name="remarks"></a>备注  
 值`RootMemberIf`元素仅供父属性 (换而言之，值[用法](usage-element-dimensionattribute-assl.md)元素的`DimensionAttribute`父元素设置为*父*) 来确定根 （父-子层次结构最顶部） 成员。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|只有符合一个或多个所述的条件的成员才*ParentIsBlank*， *ParentIsSelf*，或*ParentIsMissing*会被视为根成员。|  
|*ParentIsBlank*|仅具有 null 值、 零或空字符串所表示的键列中的成员[KeyColumns](../collections/columns-element-assl.md)的集合`DimensionAttribute`会被视为根成员。|  
|*ParentIsSelf*|只有本身作为父级的成员才会被视为根成员。|  
|*ParentIsMissing*|只有无法找到其父级的成员才会被视为根成员。|  
  
 与允许的值相对应的枚举`RootMemberIf`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.RootIfValue>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
