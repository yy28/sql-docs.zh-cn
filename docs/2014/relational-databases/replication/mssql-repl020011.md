---
title: MSSQL_REPL020011 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL020011 error
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 646f25740ebb007f8d04a89690d3b712781efcc8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060714"
---
# <a name="mssql_repl020011"></a>MSSQL_REPL020011
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20011|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|进程无法在“%2”上执行“%1”。|  
  
## <a name="explanation"></a>说明  
 在事务复制处理期间，可能会在很多情况下引发此错误，例如，当日志读取器代理执行时**sp_replcmds** （进程无法在上执行 "sp_replcmds" \<ServerName> ）或**sp_repldone** （进程无法在上执行 "sp_repldone" \<ServerName> ）。  
  
## <a name="user-action"></a>用户操作  
 如果在您刚刚从备份中还原的数据库中出现此错误，请确保遵守了备份和还原文档中列出的步骤，包括在适合时执行 **sp_replrestart** 。 有关详细信息，请参阅 [快照复制和事务复制的备份和还原策略](administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)。  
  
 此错误是一个内部处理错误，如果在还原之外的环境中出现此错误，则通常表示必须删除或重新配置复制。 如果无法删除复制，请与客户支持部门联系以获取帮助。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [sp_replcmds (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql)   
 [sp_repldone (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql)  
  
  
