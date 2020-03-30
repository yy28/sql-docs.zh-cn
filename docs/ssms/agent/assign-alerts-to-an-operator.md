---
title: 向操作员分配警报
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- assigning alerts to operator
- SQL Server Agent, alerts
- alerts [SQL Server], assigning to operator
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: aa818155-6fa2-4565-a09f-5c7e31c89754
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 30e89871b53c7972f0c21378e9e5a49ba12d4d63
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252680"
---
# <a name="assign-alerts-to-an-operator"></a>向操作员分配警报

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题介绍如何使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中向操作员分配 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 代理警报，以便他们可以接收有关作业的通知。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>开始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制和局限  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供一种简单的图形方法来管理整个警报系统。 建议使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 配置警报基本结构。  
  
-   若要发送响应警报的通知，必须首先配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理以发送邮件。 有关详细信息，请参阅 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
-   如果在发送电子邮件或寻呼通知时出现故障，则该故障将被记录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务错误日志中。  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
只有 **sysadmin** 固定服务器角色的成员才能向操作员分配警报。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-assign-alerts-to-an-operator"></a>为操作员分配警报  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要向其分配警报的操作员的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”** 。  
  
3.  单击加号以展开 **“操作员”** 文件夹。  
  
4.  右键单击要为其分配警报的操作员，再选择“属性”  ，然后选择“通知”  页。  
  
5.  在“_operator\_name_ 属性”  对话框的“选择页”  下，选择“通知”  。  
  
6.  在 **“按以下方式查看发送给此用户的通知”** 下，选择 **“警报”** 查看发送给此操作员的警报列表或选择 **“作业”** 查看向此操作员发送通知的作业列表。 选中下列一个或多个复选框来根据需要定义每个通知的通知方法：“电子邮件”  、“寻呼程序”  或“Net send”  。  
  
7.  完成后，单击 **“确定”** 。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-assign-alerts-to-an-operator"></a>为操作员分配警报  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行”  。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists
    -- and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_add_notification (TRANSACT-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)。  
  
