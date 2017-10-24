---
title: "MDSCHEMA_MEASUREGROUPS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_MEASUREGROUPS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d39a7ce85ec5c4781d69d5a0bcd2fb468dd701bc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 行集
  介绍数据库中的度量值组。  
  
## <a name="rowset-columns"></a>行集列  
 **MDSCHEMA_MEASUREGROUPS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此度量值组所属的目录的名称。 **NULL**如果提供程序不支持目录。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||不提供支持。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此度量值组所属的多维数据集的名称。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||度量值组的名称。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||用户可以阅读的成员说明。|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**||一个布尔值，指示度量值组是否已启用写操作。<br /><br /> 返回**true**如果度量值组启用写功能。|  
|**MEASUREGROUP_CAPTION**|**DBTYPE_WSTR**||度量值组的显示标题。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **MDSCHEMA_MEASUREGROUPS**行集可限制下表中的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|可选。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|可选。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

