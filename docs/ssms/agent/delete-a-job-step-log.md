---
title: "删除作业步骤日志 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server Agent]
- deleting job step logs
- logs [SQL Server], jobs
- removing job step logs
ms.assetid: ee20c6cd-0258-4550-bdb0-71e86a0fb330
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 843f2c327a287c6c879f9746321acb3407080da9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="delete-a-job-step-log"></a>Delete a Job Step Log
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主题介绍如何删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业步骤日志。  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要删除 SQL Server 代理作业步骤日志，可使用：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理对象](#SMO)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
删除作业步骤时，将自动删除其输出日志。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>删除 SQL Server 代理作业步骤日志  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”，再展开“作业”，然后右键单击要修改的作业，再单击“属性”。  
  
3.  在 **“作业属性”** 对话框中，删除所选作业步骤。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>删除 SQL Server 代理作业步骤日志  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- removes the job step log for step 2 in the job Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobsteplog  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 2;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_delete_jobsteplog (Transact-SQL)](http://msdn.microsoft.com/en-us/e9ef4c99-abde-4038-b6a3-a25dcbaf0958)。  
  
## <a name="SMO"></a>使用 SQL Server 管理对象  
通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 **Job** 类的 **DeleteJobStepLogs** 方法。 有关详细信息，请参阅[SQL Server 管理对象 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
```  
-- Uses PowerShell to delete all job step log files that have ID values larger than 5.  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = $srv.JobServer.Jobs["Test Job"]  
$jb.DeleteJobStepLogs(5)  
```  
  
