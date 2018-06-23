---
title: 角色元素 (ASSL) |Microsoft 文档
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
- Roles Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Roles
helpviewer_keywords:
- Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f8ced51e40e2804054a0c63368622d2df70f81fc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126721"
---
# <a name="roles-element-assl"></a>Roles 元素 (ASSL)
  包含在父元素下定义的 [Role](../objects/role-element-assl.md) 元素的集合。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Database> <!-- or Server -->  
   ...  
   <Roles>  
      <Role>...</Role>  
   </Roles>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Database](../objects/database-element-assl.md)、 [Server](../objects/server-element-assl.md)|  
|子元素|[角色](../objects/role-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 与 `Roles` 元素关联的 `Server` 元素仅包含一个角色，即命名管理员，它表示服务器管理角色。 服务器管理员角色不可更改或删除，也不可向集合中添加其他角色。  
  
 与 `Roles` 元素关联的 `Database` 元素包含为该数据库定义的角色。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.RoleCollection>。  
  
## <a name="see-also"></a>请参阅  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  