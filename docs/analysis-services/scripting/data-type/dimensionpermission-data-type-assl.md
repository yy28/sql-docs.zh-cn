---
title: "DimensionPermission 数据类型 (ASSL) |Microsoft 文档"
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
- DimensionPermission Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DimensionPermission data type
ms.assetid: 066405ff-903f-467a-b0d5-e58653952c52
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 12a84edf950081669776e18775d9191fe523d66c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dimensionpermission-data-type-assl"></a>DimensionPermission 数据类型 (ASSL)
  定义一个派生数据类型，该类型表示分配给数据库维度的权限。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionPermission>  
   <!-- The following elements extend Permission -->  
   <AttributePermissions>...</AttributePermissions>  
   <AllowedRowsExpression>...</AllowedRowsExpression>  
</DimensionPermission>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[权限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[AttributePermissions](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)， [AllowedRowsExpression](../../../analysis-services/scripting/collections/attributepermissions-element-assl.md)|  
|派生元素|[DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 此元素在 DeploymentMode 值 2（表格服务器模式）下具有以下验证。  
  
-   *AttributePermission*属性必须为空或发生错误。  
  
 此元素在 DeploymentMode 值 0 (OLAP) 下具有以下验证。  
  
-   *AllowedRowsExpression*属性必须为空或发生错误。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DimensionPermission>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

