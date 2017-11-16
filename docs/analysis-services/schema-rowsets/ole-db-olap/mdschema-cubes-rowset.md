---
title: "MDSCHEMA_CUBES 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_CUBES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a3fa75f9ea6bcab54d123d6e914d5d77077b44e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemacubes-rowset"></a>MDSCHEMA_CUBES 行集
  介绍数据库中的多维数据集的结构。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_CUBES**行集包含以下各列。  
  
|列名|类型指示符|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|数据库的名称。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不提供支持。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|多维数据集或维度的名称。 维度名称以美元符号 ($) 开头。<br /><br /> 注意： 仅服务器和数据库管理员有权限看到从维度创建多维数据集。|  
|**CUBE_TYPE**|**DBTYPE_WSTR**|多维数据集的类型。 有效值为<br /><br /> **多维数据集**<br /><br /> **维度**|  
|**CUBE_GUID**|**DBTYPE_GUID**|不提供支持。|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**|不提供支持。|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**|上次处理相应多维数据集的时间。|  
|**SCHEMA_UPDATED_BY**|**DBTYPE_WSTR**|不提供支持。|  
|**LAST_DATA_UPDATE**|**DBTYPE_DBTIMESTAMP**|上次处理相应多维数据集的时间。|  
|**DATA_UPDATED_BY**|**DBTYPE_WSTR**|不提供支持。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|多维数据集的用户友好说明。|  
|**IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|一个布尔值，它始终返回 true。|  
|**IS_LINKABLE**|**DBTYPE_BOOL**|一个布尔值，指示是否可以在链接多维数据集中使用多维数据集。|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**|一个布尔值，指示多维数据集是否已启用写操作。|  
|**IS_SQL_ENABLED**|**DBTYPE_BOOL**|一个布尔值，指示是否可以对多维数据集使用 SQL。|  
|**CUBE_CAPTION**|**DBTYPE_WSTR**|多维数据集的标题。|  
|**BASE_CUBE_NAME**|**DBTYPE_WSTR**|如果相应多维数据集为透视多维数据集，则为源多维数据集的名称。|  
|**批注**|**DBTYPE_WSTR**|（可选）一组格式为 XML 的注释。|  
  
 行集按排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_CUBES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（可选）默认限制是值为 1。 位图，并使用两个有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**基 Cube_Name**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

