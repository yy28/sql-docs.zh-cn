---
title: Stretch Database 扩展存储的过程 (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: stored-procedures
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c2278b57646040fe70dd154ba0c0be7d02557ff7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979369"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database 扩展存储的过程 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 本部分介绍与 Stretch Database 相关的扩展存储的过程。  
  
## <a name="in-this-section"></a>本节内容  
[sys.sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)删除本地已启用延伸的数据库和远程 Azure 数据库之间的经过身份验证的连接。

[sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)获取中临时表以帮助确保完整还原的远程 Azure 数据库，如果没有必要进行还原的 SQL Server 保留的已迁移数据的小时数。
  
 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md)还原启用了 Stretch 的本地数据库和远程数据库之间的经过身份验证的连接。
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 协调与存储在远程 Azure 表中的批处理 ID 存储在最近迁移的数据的已启用延伸的 SQL Server 表中的批处理 ID。 
 
[sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md)协调远程 Azure 表中的列中的列已启用延伸的 SQL Server 表。
 
 [sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md)排队以对帐远程表的索引的架构任务。
 
 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)指定针对当前已启用延伸的数据库和其表的查询返回本地和远程数据 （默认值） 或仅限本地数据。
 
 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md)设置的 SQL Server 保留的已迁移数据的小时数中临时表以帮助确保完整还原的远程 Azure 数据库，如果没有必要进行还原。
 
 [sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md)测试从 SQL Server 与远程 Azure 服务器的连接，并报告可能会阻止数据迁移的问题。
 
## <a name="see-also"></a>请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
