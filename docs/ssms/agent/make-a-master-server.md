---
title: 设置主服务器 | Microsoft Docs
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
f1_keywords:
- sql13.ag.msxwiz.operator.f1
- sql13.ag.msxwiz.login.f1
- sql13.ag.msxwiz.target.f1
- sql13.ag.msxwiz.complete.f1
- sql13.ag.msxwiz.cover.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 12fe6ba1182f5ad4cfa60176eba40a3de28971a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33045874"
---
# <a name="make-a-master-server"></a>Make a Master Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL 数据库托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支持大多数但并非所有 SQL Server 代理功能。 有关详细信息，请参阅 [Azure SQL 数据库托管实例与 SQL Server 之间的 T-SQL 差异](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主题描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 设置主服务器 [!INCLUDE[tsql](../../includes/tsql_md.md)]。  
  
**本主题内容**  
  
-   **开始之前：**  
  
    [Security](#Security)  
  
-   **若要设置主服务器，请使用：**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>开始之前  
  
### <a name="Security"></a>Security  
如果分布式作业的步骤与某个代理相关联，则该作业将在目标服务器上该代理帐户的上下文下运行。 请确保满足以下条件，否则与代理关联的作业步骤将不会从主服务器下载到目标服务器上：  
  
-   主服务器注册表子项 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) 设置为 1 (true)。 默认情况下，此子项设置为 0 (False)。  
  
-   目标服务器上已存在与运行作业步骤的主服务器代理帐户同名的代理帐户。  
  
从主服务器将使用代理帐户的作业步骤下载到目标服务器时，如果作业步骤失败，可以检查 **msdb** 数据库中 **sysdownloadlist** 表的 **error_message** 列是否存在以下错误消息：  
  
-   “该作业步骤需要代理帐户，但是目标服务器上禁用了代理匹配功能。”  
  
    若要解决此错误，请将 **AllowDownloadedJobsToMatchProxyName** 注册表子项设置为 1。  
  
-   “找不到代理。”  
  
    若要解决此错误，请确保目标服务器上已存在与运行作业步骤的主服务器代理帐户同名的代理帐户。  
  
#### <a name="Permissions"></a>Permissions  
默认情况下授予 **sysadmin** 固定服务器角色的成员执行此过程的权限。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-make-a-master-server"></a>设置主服务器  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的实例，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”，指向“多服务器管理”，再单击“将其设置为主服务器”。 **主服务器向导** 将引导您完成设置主服务器和添加目标服务器的过程。  
  
3.  从“主服务器操作员”中，配置主服务器的操作员。若要通过电子邮件或寻呼程序向操作员发送通知，必须配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理以发送电子邮件。 若要使用 **net send**向操作员发送通知，必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理所在的服务器上运行 Messenger 服务。  
  
    **电子邮件地址**  
    设置操作员的电子邮件地址。  
  
    **寻呼地址**  
    设置操作员的寻呼电子邮件地址。  
  
    **Net send 地址**  
    设置操作员的 **net send** 地址。  
  
4.  从 **“目标服务器”** 页中，为主服务器选择目标服务器。  
  
    **已注册的服务器**  
    列出已在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 中注册但尚未成为目标服务器的服务器。  
  
    **目标服务器**  
    列出已经为目标服务器的服务器。  
  
    **>**  
    将所选服务器移动到目标服务器列表中。  
  
    **>>**  
    将所有服务器移动到目标服务器列表中。  
  
    **<**  
    从目标服务器列表中删除所选服务器。  
  
    **<<**  
    从目标服务器列表中删除所有服务器。  
  
    **添加连接**  
    向目标服务器列表中添加服务器，但不注册该服务器。  
  
    **“连接”**  
    更改所选服务器的连接属性。  
  
5.  从 **“主服务器登录凭据”** 页中，指定是否要在必要时为目标服务器创建新的登录名，并为其分配针对主服务器的权限。  
  
    **在必要时创建新登录名，并为其分配针对 MSX 的权限**  
    如果指定的登录名不存在，则在目标服务器上创建新登录名。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-make-a-master-server"></a>设置主服务器  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde_md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 本示例将当前服务器登记到 AdventureWorks1 主服务器中。 当前服务器的位置是 Building 21、Room 309、Rack 5。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
有关详细信息，请参阅 [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)。  
  
## <a name="see-also"></a>另请参阅  
[创建多服务器环境](../../ssms/agent/create-a-multiserver-environment.md)  
[企业范围的自动化管理](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
