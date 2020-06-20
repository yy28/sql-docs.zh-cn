---
title: 更改 SQL Server 代理主作业计划的详细信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: f5414451-4d8e-464b-bd9e-f2b70c6899b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 85546bc93e6626bfcc85a28f06a4c2fe24fe9fd1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995673"
---
# <a name="change-the-scheduling-details-for-a-sql-server-agent-master-job"></a>Change the Scheduling Details for a SQL Server Agent Master Job
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中更改作业定义计划的详细信息。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要更改作业定义计划的详细信息，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理主作业不能同时把本地服务器和远程服务器作为目标。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>更改作业定义计划的详细信息  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要编辑其计划的作业的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以便展开 **“作业”** 文件夹。  
  
4.  右键单击要编辑其计划的作业，然后选择“属性”****。  
  
5.  在 "**作业属性-**_job_name_ " 对话框中的 "**选择页**" 下，选择 "**计划**"。 有关此页上可用选项的详细信息，请参阅[作业属性：新建作业 &#40;计划页&#41;](job-properties-new-job-schedules-page.md)。  
  
6.  完成后，单击“确定”****。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-change-the-scheduling-details-for-a-job-definition"></a>更改作业定义计划的详细信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- changes the enabled status of the NightlyJobs schedule to 0   
    -- and sets the owner to terrid.   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_schedule  
        @name = 'NightlyJobs',  
        @enabled = 0,  
        @owner_login_name = 'terrid' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_update_schedule ](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)。  
  
  
