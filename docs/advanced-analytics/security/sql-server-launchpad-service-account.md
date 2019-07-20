---
title: SQL Server Launchpad 服务帐户配置
description: 如何在 SQL Server 上修改用于外部脚本执行的 SQL Server Launchpad 服务帐户。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9146020fb35d729575c8441e71b711e287399a75
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345525"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server Launchpad 服务配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是一项服务, 可管理和执行外部脚本, 这与全文索引和查询服务启动单独的主机用于处理全文查询的方式类似。

有关详细信息, 请参阅[扩展性体系结构](../../advanced-analytics/concepts/extensibility-framework.md#launchpad)中的快速启动板部分 SQL Server 机器学习服务和[SQL Server 机器学习服务中的扩展性框架安全概述](../../advanced-analytics/concepts/security.md#launchpad)。

## <a name="account-permissions"></a>帐户权限

默认情况下, SQL Server Launchpad 配置为在**NT Service\MSSQLLaunchpad**下运行, 该设置具有运行外部脚本所需的所有权限。 从此帐户中删除权限可能会导致启动板无法启动或访问应运行外部脚本的 SQL Server 实例。

如果修改服务帐户, 请确保使用 "[本地安全策略" 控制台](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)。

下表列出了此帐户所需的权限。

| 组策略设置 | 常量名称 |
|----------------------|---------------|
| [调整进程的内存配额](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [绕过遍历检查](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [作为服务登录](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [替换进程级令牌](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

若要深入了解运行 SQL Server 服务所需的权限，请参阅[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>配置属性

通常, 没有理由修改服务配置。 可以更改的属性包括服务帐户、外部进程计数 (默认为 20) 或辅助角色帐户的密码重置策略。

1. 打开 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。

2. 在 "SQL Server 服务" 下, 右键单击 SQL Server Launchpad 并选择 "**属性**"。
  + 若要更改服务帐户, 请单击 "**登录**" 选项卡。
  + 若要增加用户数量, 请单击 "**高级**" 选项卡并更改 "**安全上下文计数**"。

> [!Note]
> 在早期版本的 SQL Server 2016 R Services 中, 你可以通过编辑[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]配置文件来更改服务的某些属性。 此文件不再用于更改配置。 SQL Server 配置管理器是对服务配置进行更改的正确方法, 如服务帐户和用户的数量。

## <a name="debug-settings"></a>调试设置

有些属性只能通过使用快速启动板的配置文件进行更改, 这在有限的情况下 (例如调试) 可能会很有用。 配置文件是在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装过程中创建的, 默认情况下, 该文件在中`<instance path>\binn\rlauncher.config`保存为纯文本文件。

你必须是运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的管理员才能对此文件进行更改。 如果你要编辑该文件，我们建议你在保存更改之前创建备份副本。

下表列出了的高级设置[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 以及允许的值。

|**设置名称**|**类型**|**说明**|
|----|----|----|
|退出\_时\_的\_作业清理|Integer |这只是一个内部设置-不要更改此值。 </br></br>指定是否应在会话完成后清理为每个外部运行时会话创建的临时工作文件夹。 此设置有助于调试。 </br></br>支持的值为**0** (禁用) 或**1** (已启用)。 </br></br>默认值为 1, 表示在退出时删除日志文件。|
|跟踪\_级别|Integer |出于调试目的配置 MSSQLLAUNCHPAD 的跟踪详细级别。 这会影响 LOG_DIRECTORY 设置指定的路径中的跟踪文件。 </br></br>支持的值为：**1** (错误), **2** (性能), **3** (警告), **4** (信息)。 </br></br>默认值为 1, 表示仅输出错误。|

所有设置采用键-值对的格式，每项设置单独占用一行。 例如, 若要更改跟踪级别, 可以添加行`Default: TRACE_LEVEL=4`。

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>强制执行密码策略

如果组织中的某个策略要求定期更改密码，你可能需要强制 Launchpad 服务重新生成 Launchpad 为其辅助角色帐户维护的已加密密码。

若要启用此设置并强制密码刷新，请在 SQL Server 配置管理器中打开 Launchpad 服务的“属性”窗格，单击“高级”，然后将“重置外部用户密码”更改为“是”。     应用此更改后，将立即为所有用户帐户重新生成密码。 若要在此更改后运行外部脚本, 必须重新启动启动板服务, 此时将读取新生成的密码。

若要定期重置密码，可以手动设置此标志或使用脚本。

## <a name="next-steps"></a>后续步骤

+ [扩展性框架](../concepts/extensibility-framework.md)
+ [安全性概述](../concepts/security.md)
