---
title: "将数据批量加载到合并发布的表中 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e89e68555211c6e19473b7ee915182a0d1fbd5d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>将数据批量加载到合并发布的表中
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用 [bcp Utility](../../tools/bcp-utility.md) 或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 命令将数据加载到表时，默认情况下，不会触发在 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 系统表中保留跟踪数据的合并复制触发器。 可以在加载数据时强制触发合并复制触发器，也可以使用复制存储过程，在大容量复制操作之后以编程方式插入生成的复制元数据。  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>使用 bcp 实用工具将数据大容量加载到合并复制所发布的表中  
  
1.  在发布服务器或订阅服务器上，执行 [bcp Utility](../../tools/bcp-utility.md) 或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 以将数据插入到使用合并复制发布的表中。  
  
2.  使用以下方法之一来确保为插入的数据生成复制元数据。  
  
    -   使用 FIRE_TRIGGERS 选项执行大容量复制。  
  
    -   对插入数据的数据库执行 [sp_addtabletocontents (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md)。 为 **@table_name**。  
  
  
