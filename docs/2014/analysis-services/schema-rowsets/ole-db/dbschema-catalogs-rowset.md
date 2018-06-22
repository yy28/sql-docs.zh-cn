---
title: DBSCHEMA_CATALOGS 行集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DBSCHEMA_CATALOGS
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: df3b146d3e1015fd4a78254be0d8a7a6083991d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015120"
---
# <a name="dbschemacatalogs-rowset"></a>DBSCHEMA_CATALOGS 行集
  标识可从数据库管理系统 (DBMS) 中访问的目录的关联物理属性。  
  
## <a name="rowset-columns"></a>行集列  
 `DBSCHEMA_CATALOGS`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|255|目录名称。 不可为 null。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||可读的表说明。|  
|`ROLES`|`DBTYPE_WSTR`||当前用户所属角色的逗号分隔列表。<br /><br /> 星号 (\*) 是包括作为角色，如果当前用户是服务器或数据库管理员。<br /><br /> 如果其中一个角色使用了动态安全性，则 `Username` 将追加到 `ROLES` 之后。|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||相应目录上次修改的日期。|  
  
 行集按 `CATALOG_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DBSCHEMA_CATALOGS`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|可选|  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 架构行集](ole-db-schema-rowsets.md)  
  
  