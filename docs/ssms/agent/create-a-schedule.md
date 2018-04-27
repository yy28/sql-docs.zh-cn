---
title: 创建计划 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
- schedules [SQL Server], jobs
ms.assetid: 8c7ef3b3-c06d-4a27-802d-ed329dc86ef3
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d45ec12af7a7e66b7a61151e716fe2be3558039b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-schedule"></a>Create a Schedule
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 、 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 SQL Server 管理对象在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]中创建 [!INCLUDE[tsql](../../includes/tsql_md.md)]代理作业的计划。  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要创建计划，可使用：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理对象](#SMO)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
有关详细信息，请参阅 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-a-schedule"></a>创建计划  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**，右键单击 **“作业”**，然后单击 **“管理计划”**。  
  
3.  在 **“管理计划”** 对话框中，单击 **“新建”**。  
  
4.  在 **“名称”** 框中，键入新计划的名称。  
  
5.  如果不希望计划在创建后立即生效，请清除 **“启用”** 复选框。  
  
6.  对于 **“计划类型”**，请选择下列操作之一：  
  
    -   若要在 CPU 达到空闲条件时启动作业，请单击 **“CPU 空闲时启动”**。  
  
    -   如果希望反复运行计划，请单击 **“重复执行”**。 若要设置重复执行的计划，请完成对话框上的 **“频率”**、 **“每天频率”**和 **“持续时间”** 组。  
  
    -   如果希望仅运行一次计划，请单击 **“执行一次”**。 若要设置 **“执行一次”** 计划，请完成对话框上的 **“执行一次”** 组。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-create-a-schedule"></a>创建计划  
  
1.  在 **“对象资源管理器”**中，连接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    -- creates a schedule named RunOnce.   
    -- The schedule runs one time, at 23:30 on the day that the schedule is created.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
  
    GO  
    ```  
  
有关详细信息，请参阅 [sp_add_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)。  
  
## <a name="SMO"></a>使用 SQL Server 管理对象  
**创建计划**  
  
通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 **JobSchedule** 类。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
