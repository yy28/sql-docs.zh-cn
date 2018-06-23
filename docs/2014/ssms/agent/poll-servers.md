---
title: 轮询服务器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: efb1c63e6fed68dff7425145aa89f2be1f79ae84
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128900"
---
# <a name="poll-servers"></a>轮询服务器
  实现多服务器管理后，目标服务器将定期联系主服务器以上载有关已执行的作业的信息，并下载新的作业。 联系主服务器的过程称为服务器轮询，该过程按定期的轮询间隔发生。  
  
## <a name="polling-intervals"></a>轮询间隔  
 轮询间隔（默认情况下为一分钟）控制目标服务器连接到主服务器以下载指令并上载作业执行结果的频率。  
  
 当目标服务器轮询主服务器时，它从 **msdb** 数据库的 **sysdownloadlist** 表中读取分配给目标服务器的操作。 这些操作控制多服务器作业和目标服务器行为的不同方面。 操作的示例包括删除作业、插入作业、启动作业和更新目标服务器的轮询间隔。  
  
 将操作发布到 **sysdownloadlist** 表中有下面两种方式：  
  
-   使用 **sp_post_msx_operation** 存储过程显式发布。  
  
-   使用其他作业存储过程隐式发布。  
  
 如果使用作业存储过程修改多服务器作业计划或作业步骤，或者使用 SQL 分布式管理对象 (SQL-DMO) 控制多服务器作业，请在修改多服务器作业步骤或计划后发出下列命令：  
  
```  
EXECUTE msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 发出此命令将保持目标服务器与当前作业定义同步。  
  
 您不必显式发布操作，如果您使用：  
  
-   Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 控制多服务器作业。  
  
-   不修改作业计划或作业步骤的作业存储过程。  
  
 **强制目标服务器轮询主服务器**  
  
-   [SQL Server Management Studio](force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [管理事件](manage-events.md)  
  
  
