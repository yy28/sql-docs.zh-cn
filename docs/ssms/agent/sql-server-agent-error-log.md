---
title: SQL Server 代理错误日志
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 59053d57c165e8574fcfb5af54ade6c3ad5ce2e2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75230033"
---
# <a name="sql-server-agent-error-log"></a>SQL Server 代理错误日志

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 默认情况下，代理创建错误日志来记录警告和错误。 日志中显示下列警告和错误：  
  
-   警告消息，提供有关潜在问题的信息，例如“作业 \<*job_name*> 在运行时被删除”。  
  
-   错误消息，通常需要系统管理员干预，例如“无法启动邮件会话”。 可以通过 **net send**将错误消息发送给特定用户或计算机。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最多可以维护九个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志。 每个存档日志都有一个扩展名，指示该日志的相对存在时间。 例如，扩展名 .1 表示最新的存档错误日志，而扩展名 .9 表示最旧的存档错误日志。  
  
默认情况下，执行跟踪消息不写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理日志错误，因为它们会将日志填满。 如果错误日志已满，会降低选择和分析更严重的错误的能力。 因为日志会增加服务器的处理负荷，所以请务必仔细考虑是否值得将执行跟踪消息捕获到错误日志中。 通常，最好仅在调试某个特定问题时捕获所有消息。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理停止后，可以修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理错误日志的位置。 如果错误日志为空，则无法打开日志。 可以随时使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dbo.sp_cycle_agent_errorlog[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 循环访问 [ 代理日志，无需停止 ](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql?view=sql-server-2017) 代理。  
  
**查看 SQL Server 代理错误日志**  
  
-   [查看 SQL Server 代理错误日志 (SQL Server Management Studio)](../../ssms/agent/view-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**重命名 SQL Server 代理错误日志**  
  
-   [重命名 SQL Server 代理错误日志 (SQL Server Management Studio)](../../ssms/agent/rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**发送 SQL Server 代理错误消息**  
  
-   [Send SQL Server Agent Error Messages](../../ssms/agent/send-sql-server-agent-error-messages.md)  
  
**将执行跟踪消息写入到 SQL Server 代理错误日志中**  
  
-   [将执行跟踪消息写入到 SQL Server 代理错误日志中 (SQL Server Management Studio)](../../ssms/agent/write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
