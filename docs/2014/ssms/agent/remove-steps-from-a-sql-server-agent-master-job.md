---
title: 从 SQL Server 代理主作业中删除步骤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 871e6162-1221-464d-8f7f-7e454dcd9edb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 12304e532643e536981001da3886460848aec069
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127807"
---
# <a name="remove-steps-from-a-sql-server-agent-master-job"></a>Remove Steps from a SQL Server Agent Master Job
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中删除 SQL Server 代理主作业中的步骤。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要从 SQL Server 代理主作业中删除步骤，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理主作业不能同时把本地服务器和远程服务器作为目标。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>从 SQL Server 代理主作业中删除步骤  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要从中删除步骤的作业的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以便展开 **“作业”** 文件夹。  
  
4.  右键单击要从中删除步骤的作业，然后选择“属性”。  
  
5.  在“作业属性 - job_name”对话框中的“选择页”下，选择“步骤”。  
  
6.  在 **“作业步骤列表”** 下，选择要删除的作业步骤，然后单击 **“删除”**。  
  
7.  完成后，单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-remove-steps-from-a-sql-server-agent-master-job"></a>从 SQL Server 代理主作业中删除步骤  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- removes job step 1 from the job Weekly Sales Data Backup   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1 ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_delete_jobstep &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql)。  
  
  
