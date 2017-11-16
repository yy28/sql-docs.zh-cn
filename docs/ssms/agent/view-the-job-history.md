---
title: "查看作业历史记录 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], history
- viewing job history
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
- displaying job history
ms.assetid: 3bbd1556-abdb-48a3-b249-546eace76343
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: eee4f09d33d66d6280b7befcbbe11ad15446a000
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="view-the-job-history"></a>View the Job History
本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、[!INCLUDE[tsql](../../includes/tsql_md.md)] 或 SQL Server 管理对象在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中查看 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业历史记录日志。  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要查看作业历史记录日志，请使用：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理对象](#SMO)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-view-the-job-history-log"></a>查看作业历史记录日志  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**，再展开 **“作业”**。  
  
3.  右键单击一个作业，再单击 **“查看历史记录”**。  
  
4.  在日志文件查看器中，查看作业历史记录。  
  
5.  若要更新作业历史记录，请单击 **“刷新”**。 若要只查看几行，请单击 **“筛选”** 按钮并输入筛选参数。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-view-the-job-history-log"></a>查看作业历史记录日志  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- lists all job information for the NightlyBackups job.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobhistory   
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_help_jobhistory (Transact-SQL)](http://msdn.microsoft.com/en-us/a944d44e-411b-4735-8ce4-73888d4262d7)。  
  
## <a name="SMO"></a>使用 SQL Server 管理对象  
**查看作业历史记录日志**  
  
通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来调用 **Job** 类的 **EnumHistory** 方法。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
