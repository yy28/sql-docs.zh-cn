---
description: Notify an Operator of Job Status
title: Notify an Operator of Job Status
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 520495002a15790451321f486a069154e6469199
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418103"
---
# <a name="notify-an-operator-of-job-status"></a>向操作员通知作业状态
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数（但不是所有）SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 托管实例与 SQL Server 的 T-SQL 区别](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理对象在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中设置通知选项，以便 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理可向操作员发送与作业相关的通知。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>开始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
有关详细信息，请参阅[实现 SQL Server 代理安全性](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>向操作员通知作业状态  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开“SQL Server 代理”****，展开“作业”****，右键单击要编辑的作业，再选择“属性”****。  
  
3.  在 **“作业属性”** 对话框中，选择 **“通知”** 页。  
  
4.  如果想通过电子邮件通知操作员，请选中“电子邮件”****，再从列表中选择操作员，然后选择下列选项之一：  
  
    -   **当作业成功时** - 在作业成功完成后通知操作员。  
  
    -   **“当作业失败时”** - 在作业未成功完成时通知该操作员。  
  
    -   **当作业完成时** ，无论完成情况如何，都通知该操作员。  
  
5.  如果您想通过寻呼程序来通知操作员，请选中 **“寻呼程序”**，再从列表中选择操作员，然后选择下列选项之一：  
  
    -   **当作业成功时** - 在作业成功完成后通知操作员。  
  
    -   **“当作业失败时”** - 在作业未成功完成时通知该操作员。  
  
    -   **当作业完成时** ，无论完成情况如何，都通知该操作员。  
  
6.  如果想通过 net send 通知操作员，请选中 **Net send**，再从列表中选择操作员，然后选择下列选项之一：  
  
    -   **当作业成功时** - 在作业成功完成后通知操作员。  
  
    -   **“当作业失败时”** - 在作业未成功完成时通知该操作员。  
  
    -   **当作业完成时** ，无论完成情况如何，都通知该操作员。  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>向操作员通知作业状态  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists
    --  and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_add_notification (TRANSACT-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)。  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  
**向操作员通知作业状态**  
  
通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 **Job** 类。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
