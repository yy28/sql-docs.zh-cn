---
title: "列出作业类别信息 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6707983f3fe707a5253ff6722adb190579bd1d48
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="list-job-category-information"></a>列出作业类别信息
本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 SQL Server 管理对象在 [!INCLUDE[tsql](../../includes/tsql_md.md)] 中列出作业类别信息。  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要列出作业类别信息，请使用：**  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理对象](#SMO)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>列出作业类别信息  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_help_category (Transact-SQL)](http://msdn.microsoft.com/en-us/8cad1dcc-b43e-43bd-bea0-cb0055c84169)。  
  
## <a name="SMO"></a>使用 SQL Server 管理对象  
**列出作业类别信息**  
  
通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 **JobCategory** 类。  
  

