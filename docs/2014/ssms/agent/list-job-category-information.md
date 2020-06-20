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
ms.openlocfilehash: 924e2b064980b2ea7068230610414262995da1a6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008721"
---
# <a name="list-job-category-information"></a>列出作业类别信息
  如何 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用或 SQL Server 管理对象列出中的作业类别信息 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  

  
##  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  

  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>列出作业类别信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```sql
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_help_category ](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql)。  
  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  
 **列出作业类别信息**  
  
 通过使用所选的编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 `JobCategory` 类。 有关详细信息，请参阅[SQL Server 管理对象 &#40;SMO&#41; 编程指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
