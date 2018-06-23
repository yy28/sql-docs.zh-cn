---
title: MSSQL_REPL020011 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_REPL020011 error
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b4b3ceb8ea7498053b7dde311213cfb7bea5fb99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028764"
---
# <a name="mssqlrepl020011"></a>MSSQL_REPL020011
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20011|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|进程无法在“%2”上执行“%1”。|  
  
## <a name="explanation"></a>解释  
 事务复制处理过程中的许多情况都可能引发此错误，例如日志读取器代理执行 **sp_replcmds**（此过程无法在 \<服务器名> 上执行“sp_replcmds”）或 **sp_repldone**（此过程无法在 \<服务器名> 上执行“sp_repldone”）时。  
  
## <a name="user-action"></a>用户操作  
 如果在您刚刚从备份中还原的数据库中出现此错误，请确保遵守了备份和还原文档中列出的步骤，包括在适合时执行 **sp_replrestart** 。 有关详细信息，请参阅 [快照复制和事务复制的备份和还原策略](administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
 此错误是一个内部处理错误，如果在还原之外的环境中出现此错误，则通常表示必须删除或重新配置复制。 如果无法删除复制，请与客户支持部门联系以获取帮助。  
  
## <a name="see-also"></a>请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [sp_replcmds (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql)   
 [sp_repldone (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql)  
  
  
