---
title: 删除作业步骤日志 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- deleting job step logs
- logs [SQL Server], jobs
- removing job step logs
ms.assetid: ee20c6cd-0258-4550-bdb0-71e86a0fb330
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd6cefd41ea223b91445042ff3cee9090074feeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783184"
---
# <a name="delete-a-job-step-log"></a>Delete a Job Step Log
  本主题介绍如何删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业步骤日志。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要删除 SQL Server 代理作业步骤日志，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 删除作业步骤时，将自动删除其输出日志。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 权限  
 除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>删除 SQL Server 代理作业步骤日志  
  
1.  在**对象资源管理器中，** 连接到的[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”****，再展开“作业”****，然后右键单击要修改的作业，再单击“属性”****。  
  
3.  在 **“作业属性”** 对话框中，删除所选作业步骤。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>删除 SQL Server 代理作业步骤日志  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```sql
    -- removes the job step log for step 2 in the job Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobsteplog  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 2;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_delete_jobsteplog ](/sql/relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql)。  
  
##  <a name="SMO"></a>使用 SQL Server 管理对象  
 通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 `DeleteJobStepLogs` 类的 `Job` 方法。 有关详细信息，请参阅[SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
```powershell
# Delete all job step log files that have ID values larger than 5.  
$srv = New-Object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = $srv.JobServer.Jobs["Test Job"]  
$jb.DeleteJobStepLogs(5)  
```
