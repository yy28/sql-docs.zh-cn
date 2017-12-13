---
title: "DatabasePermission 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DatabasePermission Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DatabasePermission
helpviewer_keywords: DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 53c31e44901a7e0978263206b480f229224d44b2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义中的默认权限[数据库](../../../analysis-services/scripting/objects/database-element-assl.md)的特定元素[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|默认值|False|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DatabasePermissions](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|  
|子元素|[管理](../../../analysis-services/scripting/properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 只有数据库拥有的角色才能具有**DatabasePermission** 对象，并且任何角色都只能具有一个 **DatabasePermission** 对象。  
  
 此元素在 DeploymentMode 值 2（表格模型）下具有以下验证。  
  
-   除非用户具有管理权限，否则*Administer* 属性默认值设置为 **False**。 对于具有管理权限的用户，属性值设置为 **True**。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DatabasePermission>。  
  
## <a name="see-also"></a>另请参阅  
 [Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
