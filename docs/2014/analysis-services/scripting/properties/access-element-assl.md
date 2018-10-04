---
title: 访问元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 60fbf476e1d884cce28dd674ab16d3bda001a3a0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051837"
---
# <a name="access-element-assl"></a>Access 元素 (ASSL)
  指示到提供的访问级别[CellPermission](../objects/cellpermission-element-assl.md)元素。  
  
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
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CellPermission](../objects/cellpermission-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值被限制为下表中列出的字符串之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*读取*|允许只读访问权限。|  
|*有条件读取*|允许有条件读取访问。|  
|*ReadWrite*|允许读写访问。|  
  
 与允许的值相对应的枚举`Access`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.CellPermissionAccess>。  
  
## <a name="see-also"></a>请参阅  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
