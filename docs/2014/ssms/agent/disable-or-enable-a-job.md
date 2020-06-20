---
title: 禁用或启用作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- stopping jobs
- disabling jobs
- SQL Server Agent jobs, disabling
- jobs [SQL Server Agent], disabling
ms.assetid: 5041261f-0c32-4d4a-8bee-59a6c16200dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42fe7cbeed1e2ff3f93b1afef52b165a7d660ddd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064512"
---
# <a name="disable-or-enable-a-job"></a>Disable or Enable a Job
  本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中禁用 [!INCLUDE[tsql](../../includes/tsql-md.md)]代理作业。 禁用作业不会将其删除，必要时可以再次启用该作业。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要禁用或启用作业，请使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-job"></a>禁用或启用作业  
  
1.  在**对象资源管理器**中，连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**。  
  
3.  展开“作业”****，然后右键单击要禁用或启用的作业。  
  
4.  若要禁用作业，请单击 **“禁用”**。 若要启用作业，请单击 **“启用”**。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-or-enable-a-job"></a>禁用或启用作业  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- changes the name, description, and enables status of the job NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @new_name = N'NightlyBackups -- Disabled',  
        @description = N'Nightly backups disabled during server migration.',  
        @enabled = 1 ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_update_job ](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)。  
  
  
