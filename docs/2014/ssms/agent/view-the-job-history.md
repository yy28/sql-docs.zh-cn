---
title: 查看作业历史记录 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- viewing job history
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
- displaying job history
ms.assetid: 3bbd1556-abdb-48a3-b249-546eace76343
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e5aa465f477bb4153a35fdd5df2519733c6cf1de
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43812243"
---
# <a name="view-the-job-history"></a>View the Job History
  本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理对象在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中查看 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业历史记录日志。  
  
-   **开始之前：**  
  
     [Security](#Security)  
  
-   **若要查看作业历史记录日志，请使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-job-history-log"></a>查看作业历史记录日志  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**，再展开 **“作业”**。  
  
3.  右键单击一个作业，再单击 **“查看历史记录”**。  
  
4.  在日志文件查看器中，查看作业历史记录。  
  
5.  若要更新作业历史记录，请单击 **“刷新”**。 若要只查看几行，请单击 **“筛选”** 按钮并输入筛选参数。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-job-history-log"></a>查看作业历史记录日志  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- lists all job information for the NightlyBackups job.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobhistory   
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_help_jobhistory &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理对象  
 **查看作业历史记录日志**  
  
 通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来调用 `EnumHistory` 类的 `Job` 方法。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
