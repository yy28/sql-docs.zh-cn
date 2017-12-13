---
title: "使用错误号创建警报 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- alerts [SQL Server], error numbers
ms.assetid: 03dd7fac-5073-4f86-babd-37e45a86023c
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6c3313c7af9cc115e69ba2d81e3f9436ae57e9f5
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="create-an-alert-using-an-error-number"></a>使用错误号创建警报
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主题介绍如何通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)] 创建在出现特定编号的错误时在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中引发的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理警报。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用错误号创建警报，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 提供了一种易用的图形方式来管理整个警报系统，这也是配置警报基础结构的推荐方式。  
  
-   用 **xp_logevent** 生成的事件在 master 数据库中发生。 因此，除非警报的 **xp_logevent** 为 **@database_name** 或 NULL，否则 **@database_name** 不触发警报。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
默认情况下，只有 **sysadmin** 固定服务器角色的成员才能执行 **sp_add_alert**。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>使用错误号创建警报  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要使用错误号创建警报的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  右键单击“警报”并选择“新建警报”。  
  
4.  在 **“新建警报”** 对话框的 **“名称”** 框中，输入此警报的名称。  
  
5.  选中 **“启用”** 复选框将运行警报。 默认情况下， **“启用”** 为选中状态。  
  
6.  在 **“类型”** 列表中，选择 **“SQL Server 事件警报”**。  
  
7.  在 **“事件警报定义”**下的 **“数据库名称”** 列表中，选择一个数据库以将警报限制到特定数据库。  
  
8.  在 **“将根据以下条件触发警报”**下，单击 **“错误号”**，然后为警报键入有效的错误号。 或者，单击 **“严重性”** ，然后选择将引发警报的特定严重性。  
  
9. 选中与 **“当消息包含以下内容时触发警报”** 复选框以将警报限制到特定的字符序列，然后在 **“消息正文”**中输入关键字或字符串。 最大字符数为 100。  
  
10. 单击 **“确定”**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>使用错误号创建警报  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 **“执行”**。  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up
    -- the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up
    -- the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The DB will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_add_alert (Transact-SQL)](http://msdn.microsoft.com/en-us/d9b41853-e22d-4813-a79f-57efb4511f09)。  
  
