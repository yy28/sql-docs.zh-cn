---
title: 修改作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 614c35992be2f85ef15afd0645140746041d083d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62656367"
---
# <a name="modify-a-job"></a>Modify a Job
  本主题说明如何使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 SQL Server 管理对象在中更改代理作业的属性。  
  
 **本主题内容**  
  
-   **开始之前：** ，  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要修改作业，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理主作业不能同时把本地服务器和远程服务器作为目标。  
  
###  <a name="Security"></a> Security  
 除非您是 **sysadmin** 固定服务器角色的成员，否则您只能修改自己拥有的作业。 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>修改作业  
  
1.  在**对象资源管理器中，** 连接到的[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”****，再展开“作业”****，然后右键单击要修改的作业，再单击“属性”****。  
  
3.  在 **“作业属性”** 对话框中，使用相应的页来更新作业的属性、步骤、计划、警报和通知。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-a-job"></a>修改作业  
  
1.  在对象资源管理器中，连接到数据库引擎实例，然后展开该实例。  
  
2.  在工具栏上，单击“新建查询”****。  
  
3.  在查询窗口中，使用以下系统存储过程修改作业。  
  
    -   执行[sp_update_job &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) ，以更改作业的属性。  
  
    -   执行[sp_update_schedule &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql) ，以更改作业定义的计划详细信息。  
  
    -   执行[&#40;transact-sql&#41;sp_add_jobstep](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) ，以添加新的作业步骤。  
  
    -   执行[sp_update_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) ，以更改预先存在的作业步骤。  
  
    -   执行[sp_delete_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql) ，以便从作业中删除作业步骤。  
  
    -   修改任何 SQLServer 代理主作业的其他存储过程：  
  
        -   执行[sp_delete_jobserver &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql)删除当前与作业相关联的服务器。  
  
        -   执行[sp_add_jobserver &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql) ，将服务器与当前作业相关联。  
  
##  <a name="SMO"></a>使用 SQL Server 管理对象  
 **修改作业**  
  
 通过使用所选的编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 `Job` 类。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
