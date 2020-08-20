---
description: 'sys. pdw_table_distribution_properties (Transact-sql) '
title: sys. pdw_table_distribution_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 580ce1c29f8c788e23cac3d2c78edf164118cb6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475322"
---
# <a name="syspdw_table_distribution_properties-transact-sql"></a>sys. pdw_table_distribution_properties (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存表的分发信息。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|为其指定三个属性的表的 ID。||  
|**distribution_policy**|**tinyint**|0 = 未定义<br /><br /> 1 = 无<br /><br /> 2 = 哈希<br /><br /> 3 = 复制<br /><br /> 4 = ROUND_ROBIN||  
|**distribution_policy_desc**|**nvarchar(60)**|未定义、无、哈希、复制、ROUND_ROBIN|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 返回 HASH、ROUND_ROBIN 或复制。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
