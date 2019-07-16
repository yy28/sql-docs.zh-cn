---
title: sys.database_automatic_tuning_options (TRANSACT-SQL) |Microsoft Docs
description: 了解如何查看 SQL 数据库自动优化选项
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 437dbbc4ea7deb32a9723febb443cc67941fdc5e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67940227"
---
# <a name="sysdatabaseautomatictuningoptions-transact-sql"></a>sys.database\_自动\_tuning_options (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  返回用于此数据库的自动优化选项。  

|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|自动优化选项的名称。 请参阅[ALTER DATABASE 设置 AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)可用的选项。|  
|**desired_state**|**smallint**|指示自动优化选项，由用户显式设置的所需的操作模式。<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|自动调节选项所需的操作模式的文本说明。<br />OFF<br />ON|  
|**actual_state**|**smallint**|指示自动优化选项的操作模式。<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|自动优化选项的实际操作模式的文本说明。<br />OFF<br />ON|  
|**reason**|**smallint**|指示为什么实际和所需状态的不同。<br />2 = 已禁用<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|为什么实际和所需状态的不同的原因的文本说明。<br />已禁用 = 选项已被系统禁用<br />QUERY_STORE_OFF = Query Store 处于关闭状态<br />QUERY_STORE_READ_ONLY = 查询存储处于只读模式<br />NOT_SUPPORTED = 可用仅在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]企业版| 
  
## <a name="permissions"></a>权限  
 需要 `VIEW DATABASE STATE` 权限。  
  
## <a name="see-also"></a>请参阅  
 [自动优化](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
