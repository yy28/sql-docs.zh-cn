---
title: 访问元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Access Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Access
helpviewer_keywords:
- Access element
ms.assetid: 6ad99010-fac5-48e9-a099-ecbca380e127
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d1eea0d7e8b0d26692c2cc6e0400d4ceaf7aa8ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126613"
---
# <a name="access-element-assl"></a>Access 元素 (ASSL)
  指示提供给访问级别[CellPermission](../objects/cellpermission-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CellPermission>  
   ...  
   <Access>...</Access>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CellPermission](../objects/cellpermission-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值被限制为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*读取*|允许只读访问。|  
|*ReadContingent*|允许有条件读取访问。|  
|*ReadWrite*|允许读写访问。|  
  
 对应于的允许值为枚举`Access`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.CellPermissionAccess>。  
  
## <a name="see-also"></a>请参阅  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  