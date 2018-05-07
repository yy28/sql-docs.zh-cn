---
title: MDSCHEMA_MEASUREGROUPS 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00748d265b11ea9c97b60428ac3195235efb3f8b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB for OLAP 架构行集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
