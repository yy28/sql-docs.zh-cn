---
title: 将作业所有权授予其他人 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5245bd58ab52af1383cf056ac583729968d79162
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203097"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
  本主题介绍如何将 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业的所有权重新指派给另一用户。  
  
-   **准备工作：**[限制和局限](#Restrictions)、[安全性](#Security)  
  
-   **若要将作业所有权授予其他人，请使用：**  
  
     [SQL Server Management Studio](#SSMSProc2)  
  
     [Transact-SQL](#TsqlProc2)  
  
     [SQL Server 管理对象](#SMOProc2)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
 若要创建作业，用户必须是某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色或 **sysadmin** 固定服务器角色的成员。 作业只能由其所有者或 **sysadmin** 角色的成员进行编辑。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的固定数据库角色的详细信息，请参阅 [SQL Server 代理固定数据库角色](sql-server-agent-fixed-database-roles.md)。  
  
 您必须是系统管理员才可以更改作业的所有者。  
  
 将作业指派给另一个登录名并不保证新所有者有足够的权限来成功运行该作业。  
  
###  <a name="Security"></a> 安全性  
 为了安全起见，仅作业所有者或 **sysadmin** 角色的成员可以更改作业的定义。 只有 **sysadmin** 固定服务器角色的成员才可以将作业所有权分配给其他用户，并且他们可以运行任何作业，而不管作业所有者是谁。  
  
> [!NOTE]  
>  如果将作业所有权重新指派到的用户不是 **sysadmin** 固定服务器角色的成员，而执行作业的步骤需要代理帐户（例如， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包执行），则请确保该用户可以访问该代理帐户，否则作业将失败。  
  
####  <a name="Permissions"></a> Permissions  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)。  
  
##  <a name="SSMSProc2"></a> 使用 SQL Server Management Studio  
 **将作业所有权授予其他人**  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”，再展开“作业”，右键单击相应作业，然后单击“属性”。  
  
3.  在 **“所有者”** 列表中，选择一个登录名。 您必须是系统管理员才可以更改作业的所有者。  
  
     将作业指派给另一个登录名并不保证新所有者有足够的权限来成功运行该作业。  
  
##  <a name="TsqlProc2"></a> 使用 Transact-SQL  
 **将作业所有权授予其他人**  
  
1.  在对象资源管理器中，连接到数据库引擎实例，然后展开该实例。  
  
2.  在工具栏上，单击 **“新建查询”**。  
  
3.  在查询窗口中，输入下面的语句，使用[sp_manage_jobs_by_login &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-manage-jobs-by-login-transact-sql)系统存储过程。 以下示例将所有作业从 `danw` 重新分配给 `françoisa`。  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'françoisa' ;  
    GO  
    ```  
  
##  <a name="SMOProc2"></a> 使用 SQL Server 管理对象  
 **将作业所有权授予其他人**  
  
1.  调用`Job`类通过使用一种编程语言的选择，如 Visual Basic、 Visual C# 或 PowerShell。 有关示例代码，请参阅 [在 SQL Server 代理中计划自动管理任务](sql-server-agent.md)。  
  
## <a name="see-also"></a>请参阅  
 [执行作业](implement-jobs.md)   
 [创建作业](create-jobs.md)  
  
  
