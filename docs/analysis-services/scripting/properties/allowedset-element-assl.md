---
title: AllowedSet 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0d770778f0ba887405eb7184593ed2a63cf21bb7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="allowedset-element-assl"></a>AllowedSet 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含定义的允许权限集是集表达式[角色](../../../analysis-services/scripting/objects/role-element-assl.md)特性的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributePermission>  
      ...  
   <AllowedSet>...</AllowedSet>  
   ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**AllowedSet**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AttributePermission>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
