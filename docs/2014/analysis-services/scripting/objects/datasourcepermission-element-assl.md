---
title: DataSourcePermission 元素 (ASSL) |Microsoft Docs
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
- DataSourcePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSourcePermission element
ms.assetid: 6dc6fb13-034e-479a-902e-27f3fb78c33f
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d88f18a752e96e5081462056d831bc968dc605df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241357"
---
# <a name="datasourcepermission-element-assl"></a>DataSourcePermission 元素 (ASSL)
  定义中的默认权限[数据源](../data-type/datasource-data-type-assl.md)特定的数据类型[角色](role-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSourcePermissions>  
   <DataSourcePermission xsi:type="Permission">  
      <!-- No child elements other than those from Permission are defined -->  
...</DataSourcePermission>  
</DataSourcePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[权限](../data-type/permission-data-type-assl.md)|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可出现一次或多次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSourcePermissions](../collections/datasourcepermissions-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 只有数据库拥有的角色才能具有 `DataSourcePermission` 对象，并且任何角色都只能具有一个 `DataSourcePermission` 对象。  
  
## <a name="see-also"></a>请参阅  
 [Role 元素&#40;ASSL&#41;](role-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
