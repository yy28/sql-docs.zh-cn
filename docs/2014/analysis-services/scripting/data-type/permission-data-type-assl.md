---
title: Permission 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Permission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Permission
helpviewer_keywords:
- Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d12fb71a8ed19ca083e8ec506fba6338f6b58a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101937"
---
# <a name="permission-data-type-assl"></a>Permission 数据类型 (ASSL)
  定义一个抽象的基元数据类型，该类型表示单个权限的相关信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Permission>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <RoleID>...</RoleID>  
   <Description>...</Description>  
   <Process>...</Process>  
   <ReadDefinition>...</ReadDefinition>  
   <Read>...</Read>  
   <Write>...</Write>  
   <Annotations>...</Annotations>  
</Permission>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|[CubePermission](../objects/cubepermission-element-assl.md)， [DatabasePermission](../objects/databasepermission-element-assl.md)， [DimensionPermission](permission-data-type-assl.md)， [MiningModelPermission](../objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[批注](../collections/annotations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[说明](../properties/description-element-assl.md)， [ID](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名称](../properties/name-element-assl.md)，[进程](../properties/process-element-assl.md)，[读取](../properties/read-element-assl.md)， [ReadDefinition](../properties/readdefinition-element-assl.md)， [RoleID](../properties/roleid-element-assl.md)，[编写](../properties/write-element-assl.md)|  
|派生元素|None|  
  
## <a name="remarks"></a>备注  
 `Permission` 充当多个派生的权限类型的实例中使用的抽象基类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 此数据类型在 DeploymentMode 值 2（表格服务器模式）下具有以下验证。  
  
-   *进程*属性默认值设置为`False`，除非用户具有**刷新**权限。 具有的用户**刷新**权限*进程*属性值设置为`True`。  
  
-   *ReadDefinition*属性值设置为`None`; 任何其他值将生成错误。  
  
-   *读取*属性值设置为`Allowed`具有的用户**用户**权限并对其`None`向用户分配**刷新**权限; 如果用户已**用户**并**刷新**权限，则该属性设置为`Allowed`。 对于具有管理权限的用户，属性值设置为 `Allowed`。  
  
-   *编写*属性值设置为`None`; 任何其他值将生成错误。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>请参阅  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
