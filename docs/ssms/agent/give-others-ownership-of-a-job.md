---
title: 将作业所有权授予其他人 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3ba025ae882c1779cc4022b4cb75d323384a2708
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题介绍如何将 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理作业的所有权重新指派给另一用户。  
  
-   **准备工作：**[限制和局限](#Restrictions)、[安全性](#Security)  
  
-   **若要将作业所有权授予其他人，请使用：**  
  
    [SQL Server Management Studio](#SSMSProc2)  
  
    [Transact-SQL](#TsqlProc2)  
  
    [SQL Server 管理对象](#SMOProc2)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
若要创建作业，用户必须是某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理固定数据库角色或 **sysadmin** 固定服务器角色的成员。 作业只能由其所有者或 **sysadmin** 角色的成员进行编辑。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理的固定数据库角色的详细信息，请参阅 [SQL Server 代理固定数据库角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
您必须是系统管理员才可以更改作业的所有者。  
  
将作业指派给另一个登录名并不保证新所有者有足够的权限来成功运行该作业。  
  
### <a name="Security"></a>Security  
为了安全起见，仅作业所有者或 **sysadmin** 角色的成员可以更改作业的定义。 只有 **sysadmin** 固定服务器角色的成员才可以将作业所有权分配给其他用户，并且他们可以运行任何作业，而不管作业所有者是谁。  
  
> [!NOTE]  
> 如果将作业所有权重新指派到的用户不是 **sysadmin** 固定服务器角色的成员，而执行作业的步骤需要代理帐户（例如， [!INCLUDE[ssIS](../../includes/ssis_md.md)] 包执行），则请确保该用户可以访问该代理帐户，否则作业将失败。  
  
#### <a name="Permissions"></a>Permissions  
有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMSProc2"></a>使用 SQL Server Management Studio  
**将作业所有权授予其他人**  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”，再展开“作业”，右键单击相应作业，然后单击“属性”。  
  
3.  在 **“所有者”** 列表中，选择一个登录名。 您必须是系统管理员才可以更改作业的所有者。  
  
    将作业指派给另一个登录名并不保证新所有者有足够的权限来成功运行该作业。  
  
## <a name="TsqlProc2"></a>使用 Transact-SQL  
**将作业所有权授予其他人**  
  
1.  在对象资源管理器中，连接到数据库引擎实例，然后展开该实例。  
  
2.  在工具栏上，单击 **“新建查询”**。  
  
3.  在查询窗口中，输入以下使用 [sp_manage_jobs_by_login (TRANSACT-SQL)](http://msdn.microsoft.com/en-us/832ec15a-6e92-4eb5-8c4a-af4dba79fbaa) 系统存储过程的语句。 以下示例将所有作业从 `danw` 重新分配给 `françoisa`。  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'françoisa' ;  
    GO  
    ```  
  
## <a name="SMOProc2"></a>使用 SQL Server 管理对象  
**将作业所有权授予其他人**  
  
1.  通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来调用 **Job** 类。 有关示例代码，请参阅 [在 SQL Server 代理中计划自动管理任务](http://msdn.microsoft.com/en-us/900242ad-d6a2-48e9-8a1b-f0eea4413c16)。  
  
## <a name="see-also"></a>另请参阅  
[执行作业](../../ssms/agent/implement-jobs.md)  
[创建作业](../../ssms/agent/create-jobs.md)  
  
