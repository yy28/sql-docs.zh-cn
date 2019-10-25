---
title: 列出作业类别信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dae8f1d98fb1758e9a9802883def1574bda68a78
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798206"
---
# <a name="list-job-category-information"></a>列出作业类别信息
  如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理对象在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中列出作业类别信息。  

  
##  <a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  

  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>列出作业类别信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”** 。  
  
    ```sql
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 有关详细信息，请[参阅&#40;sp_help_category transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql)。  
  
  
##  <a name="SMO"></a>使用 SQL Server 管理对象  
 **列出作业类别信息**  
  
 通过使用所选的编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 `JobCategory` 类。 有关详细信息，请[参阅&#40;SQL Server 管理对象&#41; SMO 编程指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
