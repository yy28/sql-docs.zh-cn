---
title: "为 SQL Server 代理设置服务启动帐户 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 94f718475a3b37b71864d883479848ec4058f252
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务启动帐户定义了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理在运行时所用的 Windows 帐户及其网络权限。 本主题说明了如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中通过 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 配置管理器设置 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]代理服务帐户。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [限制和局限](#Restrictions)  
  
    [Security](#Security)  
  
-   [使用 SQL Server Management Studio 为 SQL Server 代理设置服务启动帐户](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Restrictions"></a>限制和局限  
  
-   从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]开始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理不再要求服务启动帐户为 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Administrators 组的成员。 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务启动帐户必须是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]sysadmin 固定服务器角色的成员。 如果使用多服务器作业处理，帐户还必须是主服务器上 msdb 数据库角色 TargetServersRole 的成员。  
  
-   “对象资源管理器”仅在您拥有使用权限时才显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理节点。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中，必须将 **代理配置为使用** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]固定服务器角色的成员帐户的凭据，才能执行其功能。 该帐户必须拥有以下 Windows 权限：  
  
-   以服务身份登录 (SeServiceLogonRight)  
  
-   替换进程级别标记 (SeAssignPrimaryTokenPrivilege)  
  
-   跳过遍历检查 (SeChangeNotifyPrivilege)  
  
-   调整进程的内存配额 (SeIncreaseQuotaPrivilege)  
  
有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务帐户所需的 Windows 权限的详细信息，请参阅 [为 SQL Server 代理服务选择帐户](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 和 [设置 Windows 服务帐户](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014)。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>为 SQL Server 代理设置服务启动帐户  
  
1.  在 **“已注册的服务器”**中，单击加号以便展开 **“数据库引擎”**。  
  
2.  单击加号以便展开 **“本地服务器组”** 文件集。  
  
3.  右键单击要设置服务启动帐户的服务器实例，然后选择“SQL Server 配置管理器…”。  
  
4.  在 **“用户帐户控制”** 对话框中，请单击 **“是”**。  
  
5.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 配置管理器的控制台窗格中，选择 **“SQL Server 服务”**。  
  
6.  在详细信息窗格中，右键单击“SQL Server 代理 (server_name)”（其中 server_name 是要更改其服务启动帐户的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理实例的名称），然后选择“属性”。  
  
7.  在“SQL Server 代理 (server_name)”的“属性”对话框的“登录”选项卡中，选择“登录身份”下的以下选项之一：  
  
    -   **内置帐户**：如果你的作业仅需要本地服务器中的资源，则选择此选项。 有关如何选择 Windows 内置帐户类型的信息，请参阅 [为 SQL Server 代理服务选择帐户](http://msdn.microsoft.com/library/ms191543.aspx)。  
  
        > [!IMPORTANT]  
        > [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务不支持 **中的** Local Service [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]帐户。  
  
    -   **本帐户**：如果作业需要网络上的资源（包括应用程序资源），如果要将事件转发到其他 Windows 应用程序日志，或者如果要通过电子邮件或寻呼程序来通知操作员，则选择此选项。  
  
        如果您选择此选项：  
  
        1.  在 **“帐户名称”** 框中，输入将用来运行 SQL Server 代理的帐户。 或者，单击 **“浏览”** 打开 **“选择用户或组”** 对话框并选择要使用的帐户。  
  
        2.  在 **“密码”** 框中，输入帐户密码。 在“确认密码”框中重新输入密码。  
  
8.  单击“确定” 。  
  
9. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 配置管理器中，单击 **“关闭”** 按钮。  
  
