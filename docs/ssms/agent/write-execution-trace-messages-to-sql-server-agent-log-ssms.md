---
title: 将执行跟踪消息写入 SQL Server 代理错误日志 | Microsoft Docs
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
- logs [SQL Server], SQL Server Agent
- writing trace messages
- traces [SQL Server], SQL Server Agent logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: 90e3731e-6fae-43db-833e-9accecdd1c03
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f8d98cb48a3aebe741b134920cfe7b82aebca9f4
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979089"
---
# <a name="write-execution-trace-messages-to-the-sql-server-agent-error-log-sql-server-management-studio"></a>Write Execution Trace Messages to the SQL Server Agent Error Log (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中将 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理配置为在其错误日志中包含执行跟踪消息。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   使用 SQL Server Management Studio 将执行跟踪消息写入 SQL Server 代理错误日志  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   “对象资源管理器”仅在您拥有使用权限时才显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理节点。  
  
-   由于此选项会导致错误日志变得非常大，因此，仅在调查特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理问题时在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理错误日志中包含执行跟踪消息。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中，必须将 **代理配置为使用** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]固定服务器角色的成员帐户的凭据，才能执行其功能。 该帐户必须拥有以下 Windows 权限：  
  
-   以服务身份登录 (SeServiceLogonRight)  
  
-   替换进程级别标记 (SeAssignPrimaryTokenPrivilege)  
  
-   跳过遍历检查 (SeChangeNotifyPrivilege)  
  
-   调整进程的内存配额 (SeIncreaseQuotaPrivilege)  
  
有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务帐户所需的 Windows 权限的详细信息，请参阅 [为 SQL Server 代理服务选择帐户](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 和 [设置 Windows 服务帐户](http://msdn.microsoft.com/309b9dac-0b3a-4617-85ef-c4519ce9d014)。  
  
## <a name="SSMSProcedure"></a>  
#### <a name="to-write-execution-trace-messages-to-the-sql-server-agent-error-log"></a>将执行跟踪消息写入到 SQL Server 代理错误日志中  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开包含要将执行跟踪消息写入到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理错误日志的服务器。  
  
2.  右键单击“SQL Server 代理”，然后选择“属性”。  
  
3.  在“SQL Server 代理属性 – server_name”对话框中，在“常规”页的“错误日志”下，选中“包含执行跟踪消息”复选框。  
  
4.  单击“确定” 。  
  
