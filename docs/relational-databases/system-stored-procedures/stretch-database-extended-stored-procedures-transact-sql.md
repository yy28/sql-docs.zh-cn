---
title: Stretch Database 扩展存储的过程 (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e302aba2baf35f7a01f7242b2fa0eaaad45ee18f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database 扩展存储的过程 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 本部分介绍适用于 Stretch Database 扩展存储的过程。  
  
## <a name="in-this-section"></a>本節內容  
[sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)中删除本地已启用延伸的数据库和远程 Azure 数据库之间的经过身份验证的连接。

[sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)获取中临时表以帮助确保远程 Azure 数据库的完整还原，如果需要还原的已迁移数据的 SQL Server 保留小时数。
  
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)还原为 Stretch 启用的本地数据库和远程数据库之间的经过身份验证的连接。
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 协调与批处理 ID 存储在远程 Azure 表存储的最近已迁移数据的已启用延伸的 SQL Server 表中的批处理 ID。 
 
[sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md)协调远程 Azure 表中的列中的列已启用延伸的 SQL Server 表。
 
 [sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md)进行对帐远程表上的索引架构任务排入队列。
 
 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)指定针对当前已启用延伸的数据库和其表的查询返回本地和远程数据 （默认值） 或仅限本地数据。
 
 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)设置中临时表以帮助确保远程 Azure 数据库的完整还原，如果需要还原的已迁移数据的 SQL Server 保留小时数。
 
 [sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md)测试从 SQL Server 与远程 Azure 服务器的连接并报告可能会阻止数据迁移的问题。
 
## <a name="see-also"></a>另请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
