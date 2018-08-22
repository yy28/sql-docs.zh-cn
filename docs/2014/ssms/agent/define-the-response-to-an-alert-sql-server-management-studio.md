---
title: 定义对警报的响应 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], responding to
- responding to alerts
ms.assetid: c86ca6eb-c59f-46e9-bc32-d474e7c3b170
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ea3859dd3bc94d8d42c0ed1748091678b5b70f4
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392919"
---
# <a name="define-the-response-to-an-alert-sql-server-management-studio"></a>定义对警报的响应 (SQL Server Management Studio)
  本主题介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中定义 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报的响应方式。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要定义对警报的响应，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   在 **的未来版本中，将从** 代理中删除寻呼程序和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net send [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项。 请避免在新的开发工作中使用这些功能，并考虑修改当前使用这些功能的应用程序。  
  
-   请注意，若要向操作员发送电子邮件和寻呼通知，必须将 SQL Server 代理配置为使用数据库邮件。 有关详细信息，请参阅 [向操作员分配警报](assign-alerts-to-an-operator.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 只有 **sysadmin** 固定服务器角色的成员才能定义对警报的响应。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-define-the-response-to-an-alert"></a>定义对警报的响应  
  
1.  在 **“对象资源管理器”** 中，单击加号以便展开包含您要对其定义响应的警报的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  单击加号以展开 **“警报”** 文件夹。  
  
4.  右键单击要对其定义响应的警报，然后选择“属性”。  
  
5.  在“alert_name警报属性”对话框的“选择页”下，选择“响应”。  
  
6.  选中 **“执行作业”** 复选框，然后从 **“执行作业”** 复选框下的列表中选择出现警报时执行的作业。 您可以单击 **“新建作业”** 来创建新的作业。 也可以单击 **“查看作业”** 查看有关作业的详细信息。 若要深入了解“新建作业”和“作业属性job_name”对话框中的可用选项，请参阅[创建作业](create-a-job.md)和[查看作业](view-a-job.md)。  
  
7.  如果要在激活警报时通知操作员，请选中 **“通知操作员”** 复选框。 在“操作员”列表中，选择以下用于通知操作员的一个或多个方法：“电子邮件”、“寻呼程序”或“Net Send”。 您可以单击 **“新建操作员”** 创建新的操作员。 也可以单击 **“查看操作员”** 查看有关操作员的详细信息。 有关 **“新建操作员”** 和 **“查看操作员属性”** 对话框中的可用选项的详细信息，请参阅 [Create an Operator](create-an-operator.md) 和 [View Information About an Operator](view-information-about-an-operator.md)。  
  
8.  完成后，单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-define-the-response-to-an-alert"></a>定义对警报的响应  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- adds an e-mail notification for Test Alert.  
    -- assumes that Test Alert already exists and that François Ajenstat is a valid operator name   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
 有关详细信息，请参阅[sp_add_notification &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)。  
  
  
