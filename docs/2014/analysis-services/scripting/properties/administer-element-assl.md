---
title: 管理元素 (ASSL) |Microsoft 文档
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
- Administer Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Administer
helpviewer_keywords:
- Administer element
ms.assetid: 52924cd6-6176-47c8-ab17-4ee0e0ce42b1
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 099e5b9283acf8da6268e8b5abaaad73049ca076
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018029"
---
# <a name="administer-element-assl"></a>Administer 元素 (ASSL)
  指示在关联的权限是否包含管理权限[数据库](../objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DatabasePermission>  
      ...  
      <Administer>...</Administer>  
   ...  
</DatabasePermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|False|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DatabasePermission](../objects/databasepermission-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Administer` 元素指示用户是否可以只对指定数据库执行管理功能。 服务器管理员角色可以对实例中包含的所有数据库执行管理功能。  
  
 对应于的父元素`Administer`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DatabasePermission>。  
  
## <a name="see-also"></a>请参阅  
 [权限数据类型&#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  