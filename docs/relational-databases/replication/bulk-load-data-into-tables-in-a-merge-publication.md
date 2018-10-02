---
title: 将数据批量加载到合并发布的表中 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc2ab453279e429f148f257f75f44f26c4e57287
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781735"
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication"></a>将数据批量加载到合并发布的表中
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 [bcp Utility](../../tools/bcp-utility.md) 或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 命令将数据加载到表时，默认情况下，不会触发在 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 系统表中保留跟踪数据的合并复制触发器。 可以在加载数据时强制触发合并复制触发器，也可以使用复制存储过程，在大容量复制操作之后以编程方式插入生成的复制元数据。  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>使用 bcp 实用工具将数据大容量加载到合并复制所发布的表中  
  
1.  在发布服务器或订阅服务器上，执行 [bcp Utility](../../tools/bcp-utility.md) 或 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 以将数据插入到使用合并复制发布的表中。  
  
2.  使用以下方法之一来确保为插入的数据生成复制元数据。  
  
    -   使用 FIRE_TRIGGERS 选项执行大容量复制。  
  
    -   对插入数据的数据库执行 [sp_addtabletocontents (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md)。 为 **@table_name**。  
  
  
