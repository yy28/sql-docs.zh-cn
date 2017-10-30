---
title: "在同步期间执行脚本（复制 Transact-SQL 编程）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: deef18b1b37375e659dd0412dd7b69f10b8a3bdf
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>在同步期间执行脚本（复制 Transact-SQL 编程）
  复制支持事务发布和合并发布的订阅服务器的按需脚本执行。 此功能可将脚本复制到复制工作目录，然后使用 **sqlcmd** 将脚本应用到订阅服务器。 默认情况下，如果在对事务发布的订阅应用脚本时发生故障，分发代理将停止。 您可以使用复制存储过程以编程的方式指定要执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>为快照发布、事务发布或合并发布的所有订阅服务器指定要运行的脚本  
  
1.  编写并测试将按需执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。  
  
2.  将此脚本文件保存到此发布的快照代理能访问的位置。  
  
3.  在发布服务器上，对发布数据库执行 [sp_addscriptexec (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md)。 指定 **@publication**，为 **@scriptfile**指定步骤 2 中创建的具有完整 UNC 路径的脚本文件名称，并为 **@skiperror**指定下列值之一：  
  
    -   **0** - 如果遇到错误，代理将停止执行脚本。  
  
    -   **1** - 遇到错误时，代理将记录错误并继续执行脚本。  
  
4.  在代理下次运行以同步订阅时，指定的脚本将在每个订阅服务器上执行。  
  
## <a name="see-also"></a>另请参阅  
 [同步数据](../../relational-databases/replication/synchronize-data.md)  
  
  

