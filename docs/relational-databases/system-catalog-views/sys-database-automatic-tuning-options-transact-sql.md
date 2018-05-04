---
title: sys.database_automatic_tuning_options (Transact SQL) |Microsoft 文档
description: 了解如何查看在 SQL 数据库上的自动优化选项
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: 24
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 6b1ddbb9fd87c91182b3e43d9ac8e89465eb77f7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys.database\_自动\_tuning_options (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  返回此数据库的自动优化选项。  

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**nvarchar(128)**|自动优化选项的名称。 请参阅[ALTER 数据库设置 AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)的可用选项。|  
|**desired_state**|**int**|指示自动优化的选项，由用户显式设置的所需的操作模式。<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|自动优化选项的所需的操作模式的文本说明。<br />OFF<br />ON|  
|**actual_state**|**int**|指示自动优化选项的操作模式。<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|自动优化选项的实际操作模式的文本说明。<br />OFF<br />ON|  
|**reason**|**int**|指示为什么实际和所需状态的不同。<br />2 = 已禁用<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|为什么实际和所需状态的不同的原因的文本说明。<br />禁用 = 选项处于禁用状态系统<br />QUERY_STORE_OFF = Query Store 处于关闭状态<br />QUERY_STORE_READ_ONLY = Query Store 处于只读模式<br />NOT_SUPPORTED = 可用仅在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition| 
  
## <a name="permissions"></a>权限  
 需要 `VIEW DATABASE STATE` 权限。  
  
## <a name="see-also"></a>另请参阅  
 [自动优化](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER 数据库集 AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
