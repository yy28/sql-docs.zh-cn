---
title: "DataSourcePermissions 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DataSourcePermissions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataSourcePermissions element
ms.assetid: 6e1cfbec-65b9-4942-a628-f7f7c891e35f
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a2f721c0905d51a9613569bffa9ac85a4673f54
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="datasourcepermissions-element-assl"></a>DataSourcePermissions 元素 (ASSL)
  包含的集合[DataSourcePermission](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)与关联的元素[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <DataSourcePermissions>  
      <DataSourcePermission>...</DataSourcePermission>  
   </DataSourcePermissions>  
   ...  
</DataSource>  
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
|父元素|[数据源](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|子元素|[DataSourcePermission](../../../analysis-services/scripting/objects/datasourcepermission-element-assl.md)|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [权限数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)   
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

