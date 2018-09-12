---
title: 管理整个企业内的作业 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adb40ead9f932e2b9de46623ab3c90f94090e28a
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809893"
---
# <a name="manage-jobs-across-an-enterprise"></a>管理整个企业内的作业
  如果在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 以外对多服务器作业定义进行了更改，则必须将更改发布到下载列表中，以便目标服务器可以再次下载更新后的作业。 为了确保目标服务器具有当前的作业定义，在更新多服务器作业后，请发布一条 INSERT 指令，如下所示：  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 若要通知目标服务器多服务器作业已被修改，必须在使用以下任一过程之后调用前一个命令：  
  
-   [sp_add_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_update_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql)  
  
-   [sp_delete_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql)  
  
-   [sp_attach_schedule (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_detach_schedule &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql)  
  
    > [!NOTE]  
    >  调用 **sp_update_job** 或 **sp_delete_job** 后不需要调用 **sp_post_msx_operation**，因为这些存储过程会自动向下载列表发布所需的更改。  
  
 以下是管理整个企业内的作业要执行的常规任务：  
  
 **检查目标服务器的状态**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)  
  
-   [SQL Server 管理对象 (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **更改作业的目标服务器**  
  
-   [SQL Server Management Studio](modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
-   [SQL Server 管理对象 (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **更改目标服务器的位置**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
-   [SQL Server 管理对象 (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **同步目标服务器的时钟**  
  
-   [SQL Server Management Studio](synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)  
  
 **强制目标服务器轮询主服务器**  
  
-   [SQL Server Management Studio](force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [管理事件](manage-events.md)  
  
  
