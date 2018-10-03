---
title: DimensionPermission 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DimensionPermission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DimensionPermission data type
ms.assetid: 066405ff-903f-467a-b0d5-e58653952c52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c783f0627ad82ae0d1f33388ad086f7eb60df82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096611"
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
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[权限](permission-data-type-assl.md)|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[AttributePermissions](../collections/attributepermissions-element-assl.md)， [AllowedRowsExpression](../collections/attributepermissions-element-assl.md)|  
|派生元素|[DimensionPermission](../objects/dimensionpermission-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 此元素在 DeploymentMode 值 2（表格服务器模式）下具有以下验证。  
  
-   *AttributePermission*属性必须为空或发生错误。  
  
 此元素在 DeploymentMode 值 0 (OLAP) 下具有以下验证。  
  
-   *AllowedRowsExpression*属性必须为空或发生错误。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DimensionPermission>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
