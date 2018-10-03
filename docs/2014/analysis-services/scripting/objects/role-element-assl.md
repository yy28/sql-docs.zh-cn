---
title: Role 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Role Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ROLE
helpviewer_keywords:
- Role element
ms.assetid: 56f52462-a7fd-4b51-a7fb-4311134439e9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 720eb01952d52e7c1b9a1ec73bae272694b1597a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084028"
---
# <a name="role-element-assl"></a>Role 元素 (ASSL)
  包含有关安全角色的信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Roles>  
      <Role>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreateTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Members>...</Members>  
      <Annotations>...</Annotations>  
   </Role>  
</Roles>  
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
|父元素|[Roles](../collections/roles-element-assl.md)|  
|子元素|[批注](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[说明](../properties/description-element-assl.md)， [ID](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[成员](../collections/members-element-assl.md)，[名称](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 角色的定义包括一些用户，这些用户是该角色的成员。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Role>。  
  
## <a name="see-also"></a>请参阅  
 [数据库元素&#40;ASSL&#41;](database-element-assl.md)   
 [服务器元素&#40;ASSL&#41;](server-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
