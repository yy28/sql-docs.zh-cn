---
title: 为 SQL Server 代理服务设置 SQL Server 连接 | Microsoft Docs
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
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7db04539f73e192e83f4577e18900312de47fbb6
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980229"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>为 SQL Server 代理服务设置 SQL Server 连接 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 在 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 中设置 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 代理和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]之间的连接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务可以使用 Windows 身份验证连接到 SQL Server 本地实例。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要为 SQL Server 代理设置 SQL Server 连接，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   “对象资源管理器”仅在您拥有使用权限时才显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理节点。  
  
-   从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]开始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理不支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证。 仅在管理早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]时才能使用这种身份验证。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中，必须将 **代理配置为使用** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]固定服务器角色的成员帐户的凭据，才能执行其功能。 该帐户必须拥有以下 Windows 权限：  
  
-   以服务身份登录 (SeServiceLogonRight)  
  
-   替换进程级别标记 (SeAssignPrimaryTokenPrivilege)  
  
-   跳过遍历检查 (SeChangeNotifyPrivilege)  
  
-   调整进程的内存配额 (SeIncreaseQuotaPrivilege)  
  
有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务帐户所需的 Windows 权限的详细信息，请参阅 [为 SQL Server 代理服务选择帐户](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 和 [设置 Windows 服务帐户](http://msdn.microsoft.com/309b9dac-0b3a-4617-85ef-c4519ce9d014)。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>设置 SQL Server 连接  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要使用到其 SQL Server 代理服务的连接进行设置的服务器。  
  
2.  右键单击“SQL Server 代理”，然后选择“属性”。  
  
3.  在“SQL Server 代理属性sever_name”对话框的“选择页”下，单击“连接”。  
  
4.  在“SQL Server 连接”下，选择“使用 Windows 身份验证”以启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理，从而使用[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] [!INCLUDE[ssDE](../../includes/ssde_md.md)] 实例。 与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 及更高版本数据库的连接需要 Windows 身份验证。  
  
