---
title: DatabasePermission 元素 (ASSL) |Microsoft 文档
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
- DatabasePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e47203616cc76fa09c0fd0658e7dad8a89c90a9b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029319"
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 元素 (ASSL)
  定义中的默认权限[数据库](database-element-assl.md)的特定元素[角色](role-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DatabasePermissions>  
      <DatabasePermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <Administer>...</Administer>  
...</DatabasePermission>  
</DatabasePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[权限](../data-type/permission-data-type-assl.md)|  
|默认值|False|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DatabasePermissions](../collections/databasepermissions-element-assl.md)|  
|子元素|[管理](../properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 只有数据库拥有的角色才能具有 `DatabasePermission` 对象，并且任何角色都只能具有一个 `DatabasePermission` 对象。  
  
 此元素在 DeploymentMode 值 2（表格模型）下具有以下验证。  
  
-   *管理*属性默认值设置为`False`，除了当用户具有管理权限。 对于具有管理权限的用户，属性值设置为 `True`。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DatabasePermission>。  
  
## <a name="see-also"></a>请参阅  
 [Role 元素&#40;ASSL&#41;](role-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  