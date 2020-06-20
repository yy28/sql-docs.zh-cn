---
title: 创建操作员 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: dfe07042f9a4b8ac595ada8b86e7bad131032700
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067792"
---
# <a name="create-an-operator"></a>创建操作员
  本主题介绍如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或在中配置用户以接收有关代理作业的通知 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要创建操作员，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   在未来版本的中，将从代理中删除寻呼程序和**net send**选项 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 请避免在新的开发工作中使用这些功能，并考虑修改当前使用这些功能的应用程序。  
  
-   请注意，若要向操作员发送电子邮件和寻呼通知，必须将 SQL Server 代理配置为使用数据库邮件。 有关详细信息，请参阅 [向操作员分配警报](assign-alerts-to-an-operator.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 只有 **sysadmin** 固定服务器角色的成员才能创建操作员。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-an-operator"></a>创建操作员  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要创建 SQL Server 代理操作员的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  右键单击“操作员”**** 文件夹，然后选择“新建操作员”****。  
  
     在 **“新建操作员”** 对话框的 **“常规”** 页上提供以下选项：  
  
     **名称**  
     更改操作员的名称。  
  
     **已启用**  
     启用操作员。 在未启用时，不会向操作员发送通知。  
  
     **电子邮件名称**  
     指定操作员的电子邮件地址。  
  
     **Net send 地址**  
     指定用于 **net send**的地址。  
  
     **寻呼电子邮件名称**  
     指定用于操作员的寻呼程序的电子邮件地址。  
  
     **寻呼值班计划**  
     设置寻呼程序处于活动状态的时间。  
  
     **星期一 - 星期日**  
     选择寻呼程序在一周中的哪些天处于活动状态。  
  
     **工作日开始**  
     选择一天之中的特定时间， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在该时间之后才可向寻呼程序发送消息。  
  
     **工作日结束**  
     选择一天之中的特定时间， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理在该时间之后不再向寻呼程序发送消息。  
  
     在 **“新建操作员”** 对话框的 **“通知”** 页上提供以下选项：  
  
     **警报**  
     查看实例中的警报。  
  
     **作业**  
     查看实例中的作业。  
  
     **警报列表**  
     列出实例中的警报。  
  
     **作业列表**  
     列出实例中的作业。  
  
     **电子邮件**  
     使用电子邮件通知此操作员。  
  
     **接收**  
     通过将电子邮件发送到寻呼地址来通知此操作员。  
  
     **Net send**  
     使用 **net send**通知此操作员。  
  
4.  在完成了新操作员的创建后，单击 **“确定”**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-operator"></a>创建操作员  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- sets up the operator information for user 'danwi.' The operator is enabled.   
    -- SQL Server Agent sends notifications by pager from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_add_operator ](/sql/relational-databases/system-stored-procedures/sp-add-operator-transact-sql)。  
  
  
