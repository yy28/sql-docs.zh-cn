---
title: "其 RootMemberIf 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: RootMemberIf Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: RootMemberIf
helpviewer_keywords: RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c5a3a75efa13710bcc00a94ed55cee407dbbbc8d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="rootmemberif-element-assl"></a>RootMemberIf 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]确定如何标识或多个根成员的父属性。  
  
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
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 值**其 RootMemberIf**元素仅由父属性 (换而言之，值[用法](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md)元素**DimensionAttribute**父元素是设置为*父*) 来确定父-子层次结构的根 （顶端） 成员。  
  
 此元素的值限定为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|只有符合一个或多个所述的条件的成员*ParentIsBlank*， *ParentIsSelf*，或*ParentIsMissing*会被视为根成员。|  
|*ParentIsBlank*|仅具有 null 值、 零或空字符串所表示的键列中的成员[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)集合**DimensionAttribute**会被视为根成员。|  
|*ParentIsSelf*|只有本身作为父级的成员才会被视为根成员。|  
|*ParentIsMissing*|只有无法找到其父级的成员才会被视为根成员。|  
  
 对应于的允许值为枚举**其 RootMemberIf**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.RootIfValue>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
