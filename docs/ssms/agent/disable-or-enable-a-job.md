---
title: "禁用或启用作业 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stopping jobs
- disabling jobs
- SQL Server Agent jobs, disabling
- jobs [SQL Server Agent], disabling
ms.assetid: 5041261f-0c32-4d4a-8bee-59a6c16200dd
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 63ab17f3ac8fb0de122b8553d2f5ce536ef3701c
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="disable-or-enable-a-job"></a>启用或禁用作业
本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 中禁用 [!INCLUDE[tsql](../../includes/tsql_md.md)]代理作业。 禁用作业不会将其删除，必要时可以再次启用该作业。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要禁用或启用作业，请使用：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-job"></a>禁用或启用作业  
  
1.  在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**。  
  
3.  展开“作业”，然后右键单击要禁用或启用的作业。  
  
4.  若要禁用作业，请单击 **“禁用”**。 若要启用作业，请单击 **“启用”**。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-disable-or-enable-a-job"></a>禁用或启用作业  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
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
  
有关详细信息，请参阅 [sp_update_job (Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623)。  
  

