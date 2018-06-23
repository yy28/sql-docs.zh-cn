---
title: 列出作业类别信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 231143d7b7fb90f8da6a614d047b98f9da22dbb0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014020"
---
# <a name="list-job-category-information"></a>列出作业类别信息
  如何列出作业类别信息中的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]或 SQL Server 管理对象。  

  
##  <a name="Security"></a> 安全性  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  

  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>列出作业类别信息  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_help_category &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql)。  
  
  
##  <a name="SMO"></a> 使用 SQL Server 管理对象  
 **列出作业类别信息**  
  
 使用`JobCategory`通过使用一种选择，如 Visual Basic、 Visual C# 或 PowerShell 编程语言的类... 有关详细信息，请参阅[SQL Server 管理对象&#40;SMO&#41;编程指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
  
  
  
