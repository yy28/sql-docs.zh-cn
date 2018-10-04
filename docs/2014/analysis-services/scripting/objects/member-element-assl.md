---
title: Member 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Member Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Member
helpviewer_keywords:
- Member element
ms.assetid: 03b4cfcb-ce87-452f-9e25-8745c0423f56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c96454974357dbdd9510b1cf6f768b6e1c487a90
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126077"
---
# <a name="member-element-assl"></a>Member 元素 (ASSL)
  包含的成员的名称[组](group-element-assl.md)元素或[角色](role-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Members>  
   <Member>  
      <Name>...</Name>  
   </Member>  
</Members>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[成员](../collections/members-element-assl.md)|  
|子元素|[名称](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 父级对应的元素`Member`在 Analysis Management Objects (AMO) 对象模型<xref:Microsoft.AnalysisServices.Group>和<xref:Microsoft.AnalysisServices.Role>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
