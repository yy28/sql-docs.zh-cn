---
title: "更改 SQL Server 代理主作业的步骤 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f1a0ee6-49ff-4080-94ca-d661daeff2a6
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 599646177ad22cb5131b0c57dc07206db66153a2
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="change-steps-of-a-sql-server-agent-master-job"></a>Change Steps of a SQL Server Agent Master Job
本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 在 [!INCLUDE[tsql](../../includes/tsql_md.md)]中更改 SQL Server 代理主作业的步骤。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要更改 SQL Server 代理主作业的步骤，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理主作业不能同时把本地服务器和远程服务器作为目标。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。 有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>更改 SQL Server 代理主作业的步骤  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要修改步骤的作业的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以便展开 **“作业”** 文件夹。  
  
4.  右键单击要修改步骤的作业，然后选择“属性”。  
  
5.  在“作业属性 – job_name”对话框中的“选择页”下，选择“步骤”。  
  
6.  单击“编辑”以便打开“作业步骤属性 - job_step_name”对话框。 有关此对话框中的可用选项的详细信息，请参阅[作业步骤属性 - 新建作业步骤（“常规”页）](../../ssms/agent/job-step-properties-new-job-step-general-page.md)和[作业步骤属性 - 新建作业步骤（“高级”页）](../../ssms/agent/job-step-properties-new-job-step-advanced-page.md)。  
  
7.  完成后，单击 **“确定”**。  
  
8.  在 “作业属性 - job_name”对话框中，单击“确定”。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>更改 SQL Server 代理主作业的步骤  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- changes the number of retry attempts for the first step
    -- of the Weekly Sales Data Backup job.   
    -- After running this example, the number of retry attempts is 10   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1,  
        @retry_attempts = 10 ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_update_jobstep (TRANSACT-SQL)](http://msdn.microsoft.com/en-us/e158802c-c347-4a5d-bf75-c03e5ae56e6b)。  
  

