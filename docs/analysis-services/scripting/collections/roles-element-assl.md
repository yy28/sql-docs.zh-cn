---
title: "角色元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Roles Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Roles
helpviewer_keywords:
- Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3c077f05af1af38b2160d07bedf3e6ae401acd0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="roles-element-assl"></a>Roles 元素 (ASSL)
  包含在父元素下定义的 [Role](../../../analysis-services/scripting/objects/role-element-assl.md) 元素的集合。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Database](../../../analysis-services/scripting/objects/database-element-assl.md)、 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|[角色](../../../analysis-services/scripting/objects/role-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 与 **Roles** 元素关联的 **Server** 元素仅包含一个角色，即命名管理员（表示服务器管理角色）。 服务器管理员角色不可更改或删除，也不可向集合中添加其他角色。  
  
 与 **Roles** 元素关联的 **Database** 元素包含为该数据库定义的角色。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.RoleCollection>。  
  
## <a name="see-also"></a>另请参阅  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
