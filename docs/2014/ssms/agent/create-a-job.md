---
title: 创建作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed3c7cf100d0105d393bb8c22bbc0d38d2e9de26
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63131529"
---
# <a name="create-a-job"></a>创建作业
  本主题说明如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理对象 (SMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中创建 SQL Server 代理作业。  
  
 若要添加可以发送到操作员的作业步骤、计划、警报和通知，请参阅“请参阅”部分中的主题的链接。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要创建作业，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SQL Server 管理对象](#SMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   若要创建作业，用户必须是某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色或 **sysadmin** 固定服务器角色的成员。 作业只能由其所有者或 **sysadmin** 角色的成员进行编辑。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的固定数据库角色的详细信息，请参阅 [SQL Server 代理固定数据库角色](sql-server-agent-fixed-database-roles.md)。  
  
-   将作业指派给另一个登录名并不保证新所有者有足够的权限来成功运行该作业。  
  
-   本地作业是由本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理进行缓存的。 因此，任何修改都会隐式强制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理重新缓存该作业。 由于直到调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_add_jobserver **时，** 代理才缓存作业，因此最后调用 **sp_add_jobserver** 将更为有效。  
  
###  <a name="Security"></a> 安全性  
  
-   您必须是系统管理员才可以更改作业的所有者。  
  
-   为了安全起见，仅作业所有者或 **sysadmin** 角色的成员可以更改作业的定义。 只有 **sysadmin** 固定服务器角色的成员才可以将作业所有权分配给其他用户，并且他们可以运行任何作业，而不管作业所有者是谁。  
  
    > [!NOTE]  
    >  如果将作业所有权重新指派到的用户不是 **sysadmin** 固定服务器角色的成员，而执行作业的步骤需要代理帐户（例如， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包执行），则请确保该用户可以访问该代理帐户，否则作业将失败。  
  
####  <a name="Permissions"></a> Permissions  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-job"></a>创建 SQL Server 代理作业  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要创建 SQL Server 代理作业的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”** 。  
  
3.  右键单击“作业”文件夹，然后选择“新建作业…”   。  
  
4.  在 **“新建作业”** 对话框的 **“常规”** 页上，修改作业的常规属性。 有关此页上的可用选项的详细信息，请参阅[作业属性和新的作业&#40;常规页&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
5.  在 **“步骤”** 页上，组织作业步骤。 有关此页上的可用选项的详细信息，请参阅[作业属性： 新建作业&#40;步骤页&#41;](job-properties-new-job-steps-page.md)  
  
6.  在 **“计划”** 页上，组织作业的计划。 有关此页上的可用选项的详细信息，请参阅[作业属性：新的作业&#40;计划页&#41;](job-properties-new-job-schedules-page.md)  
  
7.  在 **“警报”** 页上，组织作业的警报。 有关此页上的可用选项的详细信息，请参阅[作业属性：新的作业&#40;警报页&#41;](job-properties-new-job-alerts-page.md)  
  
8.  在 **“通知”** 页上，设置在作业完成时 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理要执行的操作。 有关此页上的可用选项的详细信息，请参阅[作业属性：新的作业&#40;通知页&#41;](job-properties-new-job-notifications-page.md)。  
  
9. 在 **“目标”** 页上，管理作业的目标服务器。 有关此页上的可用选项的详细信息，请参阅[作业属性：新的作业&#40;以页为目标&#41;](job-properties-new-job-targets-page.md)。  
  
10. 完成后，单击 **“确定”** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-job"></a>创建 SQL Server 代理作业  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backup';  
    GO  
    ```  
  
 有关详细信息，请参阅：  
  
-   [sp_add_job (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_add_jobserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
##  <a name="SMOProcedure"></a> 使用 SQL Server 管理对象  
 **创建 SQL Server 代理作业**  
  
 通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来调用 `Create` 类的 `Job` 方法。 有关示例代码，请参阅 [在 SQL Server 代理中计划自动管理任务](sql-server-agent.md)。  
  
##  <a name="SSMSProc2"></a>  
