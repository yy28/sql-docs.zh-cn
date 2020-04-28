---
title: 停止作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b55ca5e8f2e57e85a75f610efe4115ced0dce365
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798151"
---
# <a name="stop-a-job"></a>Stop a Job
  本主题说明如何停止[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业。 作业是 SQL Server 代理执行的一系列指定操作。  
  
-   **开始之前：** ，  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要停止作业，请使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   如果作业当前正在执行 **CmdExec** 或 **PowerShell**类型的步骤，则强制提前结束正在运行的进程（例如 MyProgram.exe）。 这可能会导致不可预知的行为，如进程正在使用的文件保持为打开状态。  
  
-   对于多服务器作业，针对该作业的 STOP 指令将发布到该作业的所有目标服务器中。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>停止作业  
  
1.  在“对象资源管理器”**** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例，然后展开此实例。  
  
2.  展开 **“SQL Server 代理”**，再展开 **“作业”**，右键单击要停止的作业，再单击 **“停止作业”**。  
  
3.  若要停止多个作业，请右键单击 **“作业活动监视器”**，然后单击 **“查看作业活动”**。 在作业活动监视器中，选择要停止的作业，右键单击所选内容，然后单击 **“停止作业”**。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
### <a name="to-stop-a-job"></a>停止作业  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```sql
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_stop_job ](/sql/relational-databases/system-stored-procedures/sp-stop-job-transact-sql)。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  

### <a name="to-stop-a-job"></a>停止作业
  
 通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来调用 `Stop` 类的 `Job` 方法。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
