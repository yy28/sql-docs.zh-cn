---
title: MDSCHEMA_INPUT_DATASOURCES 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6efa6baf40c41db7de09ebcb4e5c44990ff7e6ed
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemainputdatasources-rowset"></a>MDSCHEMA_INPUT_DATASOURCES 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  介绍数据库中定义的数据源。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_INPUT_DATASOURCES**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此数据源所属目录的名称。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||不提供支持。|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**||数据源对象的名称。|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**||数据源的类型。 有效值包括：<br /><br /> **关系**<br /><br /> **Olap**|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**||创建数据源的日期。|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**||上次修改数据源的日期和时间。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||操作的用户友好说明。|  
|**超时**|**DBTYPE_UI4**||数据源的超时值。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_INPUT_DATASOURCES**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
