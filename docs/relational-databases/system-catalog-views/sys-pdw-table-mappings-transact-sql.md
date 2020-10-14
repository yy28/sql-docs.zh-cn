---
description: 'sys.pdw_table_mappings (Transact-sql) '
title: sys.pdw_table_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/01/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1af14fe0-e562-4f48-a7f0-783f300a88ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6e1b94ea731f42890a07c7d708444a95b694b317
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034781"
---
# <a name="syspdw_table_mappings-transact-sql"></a>sys.pdw_table_mappings (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  通过 **object_id**将用户表与内部对象名称进行绑定。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar (36) **|表的物理名称。<br /><br /> **physical_name** 和 **object_id** 构成此视图的键。||  
|object_id|**int**|表的对象 ID。 请参阅 [sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **physical_name** 和 **object_id** 构成此视图的键。||  
  
## <a name="see-also"></a>另请参阅  
 [Azure Synapse Analytics 和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [sys.pdw_database_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
