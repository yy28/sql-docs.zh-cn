---
title: 向 SQL Server 代理主作业添加步骤 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9cc1e8ab-7ddc-427b-859e-203aa7e24642
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce3801d0377b65b14395a1c502cf63fc0e132d69
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="add-steps-to-a-sql-server-agent-master-job"></a>Add Steps to a SQL Server Agent Master Job
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 在 [!INCLUDE[tsql](../../includes/tsql_md.md)]中向 SQL Server 代理主作业添加步骤。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要向 SQL Server 代理主作业添加步骤，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理主作业不能同时把本地服务器和远程服务器作为目标。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。 有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-add-steps-to-a-sql-server-agent-master-job"></a>向 SQL Server 代理主作业添加步骤  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要添加步骤的作业的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以便展开 **“作业”** 文件夹。  
  
4.  右键单击要向其添加步骤的作业，然后选择“属性”。  
  
5.  在“作业属性 – job_name”对话框中的“选择页”下，选择“步骤”。 有关此页上可用选项的详细信息，请参阅[作业属性 - 新建作业（“步骤”页）](../../ssms/agent/job-properties-new-job-steps-page.md)。  
  
6.  完成后，单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-add-steps-to-a-sql-server-agent-master-job"></a>向 SQL Server 代理主作业添加步骤  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- creates a job step that changes database access to read-only for the Sales database.   
    -- specifies 5 retry attempts, with each retry to occur after a 5 minute wait.   
    -- assumes that the Weekly Sales Data Backup job already exists  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755)。  
  
