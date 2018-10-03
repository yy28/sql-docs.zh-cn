---
title: DatabasePermission 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a904f12b86d6449c11f354a790503dc1bd93ffbe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106657"
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 元素 (ASSL)
  定义中的默认权限[数据库](database-element-assl.md)元素的特定[角色](role-element-assl.md)元素。  
  
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
  
## <a name="remarks"></a>备注  
 只有数据库拥有的角色才能具有 `DatabasePermission` 对象，并且任何角色都只能具有一个 `DatabasePermission` 对象。  
  
 此元素在 DeploymentMode 值 2（表格模型）下具有以下验证。  
  
-   *管理*属性默认值设置为`False`，除非用户具有管理权限。 对于具有管理权限的用户，属性值设置为 `True`。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DatabasePermission>。  
  
## <a name="see-also"></a>请参阅  
 [Role 元素&#40;ASSL&#41;](role-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
