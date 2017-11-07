---
title: "DBSCHEMA_CATALOGS 行集 |Microsoft 文档"
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
- DBSCHEMA_CATALOGS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0632d90765112ee54de8e78a66fdefa1ff27334f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbschemacatalogs-rowset"></a>DBSCHEMA_CATALOGS 行集
  标识可从数据库管理系统 (DBMS) 中访问的目录的关联物理属性。  
  
## <a name="rowset-columns"></a>行集列  
 **DBSCHEMA_CATALOGS**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|255|目录名称。 不可为 null。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||可读的表说明。|  
|**角色**|**DBTYPE_WSTR**||当前用户所属角色的逗号分隔列表。<br /><br /> 星号 (\*) 是包括作为角色，如果当前用户是服务器或数据库管理员。<br /><br /> **用户名**追加到**角色**如果角色之一使用动态安全。|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||相应目录上次修改的日期。|  
  
 行集按排序**CATALOG_NAME**。  
  
## <a name="restriction-columns"></a>限制列  
 **DBSCHEMA_CATALOGS**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|可选|  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 架构行集合](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  

