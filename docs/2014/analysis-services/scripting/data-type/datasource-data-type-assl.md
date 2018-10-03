---
title: 数据源的数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataSource Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSource data type
ms.assetid: 05e8de8d-452d-4128-98a6-4437df227fec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0eecebc417a1ddf33f00cdaf5977ca8d3297aca7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069353"
---
# <a name="datasource-data-type-assl"></a>DataSource 数据类型 (ASSL)
  定义表示中的数据源的抽象的基元数据类型[数据库](../objects/database-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ManagedProvider>...</ManagedProvider>  
   <ConnectionString>...</ConnectionString>  
   <ConnectionStringSecurity>...</ConnectionStringSecurity>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Isolation>...</Isolation>  
   <MaxActiveConnections>...</MaxActiveConnections>  
   <Description>...</Description>  
   <Timeout>...</Timeout>  
   <Annotations>...</Annotations>  
   <DataSourcePermission>...</DataSourcePermission>  
</DataSource>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|[RelationalDataSource](datasource-data-type-assl.md)， [OlapDataSource](olapdatasource-data-type-assl.md)， [PushedDataSource](pusheddatasource-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[批注](../collections/annotations-element-assl.md)， [ConnectionString](../properties/connectionstring-element-assl.md)， [ConnectionStringSecurity](../properties/connectionstringsecurity-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DataSourcePermission](../collections/datasourcepermissions-element-assl.md)，[说明](../properties/description-element-assl.md)， [ID](../properties/id-element-assl.md)， [ImpersonationInfo](../properties/impersonationinfo-element-assl.md)，[隔离](../properties/isolation-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [ManagedProvider](../properties/managedprovider-element-assl.md)， [MaxActiveConnections](../properties/maxactiveconnections-element-assl.md)，[名称](../properties/name-element-assl.md)，[超时](../properties/timeout-element-assl.md)|  
|派生元素|None|  
  
## <a name="remarks"></a>备注  
 定义外部绑定时，`Name` 元素是可选的。 不必指定 `Name` 元素使数据源可以在多维数据集、分区等的绑定中定义。 对于 `Database` 元素中包含的数据源，`Name` 是必需的元素。  
  
 有关数据源的详细信息，请参阅 [Data Sources in Multidimensional Models](../../multidimensional-models/data-sources-in-multidimensional-models.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
