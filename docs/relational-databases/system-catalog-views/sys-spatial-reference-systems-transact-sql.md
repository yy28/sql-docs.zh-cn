---
title: sys.spatial_reference_systems (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- spatial_reference_systems_TSQL
- sys.spatial_reference_systems_TSQL
- sys.spatial_reference_systems
- spatial_reference_systems
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_reference_systems catalog view
- spatial_reference_systems
ms.assetid: 3c9bc120-67c3-463f-9e24-29fd623f25a0
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: acdf8059c75ac6bec1bdd45fc7e1d348331a7e90
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysspatialreferencesystems-transact-sql"></a>sys.spatial_reference_systems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的空间引用系统 (SRID)。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的 SRID。|  
|authority_name|**nvarchar(128)**|SRID 的授权。|  
|authorized_spatial_reference_id|**int**|由授权机构在名为给定的 SRID **authority_name**。|  
|well_known_text|**nvarchar(4000)**|SRID 的 WKT 表示形式。|  
|unit_of_measure|**nvarchar(128)**|度量单位的名称。|  
|unit_conversion_factor|**float**|以米为度量单位的长度。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
