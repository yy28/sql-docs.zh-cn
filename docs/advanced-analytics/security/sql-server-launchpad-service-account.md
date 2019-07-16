---
title: SQL Server 快速启动板服务帐户配置 SQL Server 机器学习服务
description: 如何修改用于 SQL Server 上的外部脚本执行的 SQL Server 快速启动板服务帐户。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: ad6377e73633d34b322e5f455f0dd08143c53529
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962338"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server 快速启动板服务配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]是一种服务，管理和执行外部脚本，类似于全文索引和查询服务用于处理全文查询启动单独的主机的方式。

有关详细信息，请参阅中的快速启动板部分[SQL Server 机器学习服务中的可扩展性体系结构](../../advanced-analytics/concepts/extensibility-framework.md#launchpad)和[的 SQL Server 机器学习中的可扩展性框架安全概述服务](../../advanced-analytics/concepts/security.md#launchpad)。

## <a name="account-permissions"></a>帐户权限

默认情况下，SQL Server 快速启动板配置下运行**NT Service\MSSQLLaunchpad**，其中预配了所有必需的权限来运行外部脚本。 此帐户从删除的权限可能会导致未能启动或访问 SQL Server 实例应在何处运行外部脚本的快速启动板。

如果您修改的服务帐户，请务必使用[本地安全策略控制台](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings)。

下表中列出了此帐户是必需的权限。

| 组策略设置 | 常量的名称 |
|----------------------|---------------|
| [调整进程的内存配额](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [绕过遍历检查](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [作为服务登录](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [替换进程级别标记](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

若要深入了解运行 SQL Server 服务所需的权限，请参阅[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>配置属性

通常情况下，没有理由来修改服务配置。 无法更改的属性包括服务帐户的计数外部进程 (默认情况下为 20) 或密码重置辅助角色帐户的策略。

1. 打开 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。

2. 在 SQL Server 服务、 右键单击 SQL Server 快速启动板，然后选择**属性**。
  + 若要更改服务帐户，请单击**Log On**选项卡。
  + 若要增加的用户数，请单击**高级**选项卡上，并将更改**安全上下文计数**。

> [!Note]
> 在早期版本的 SQL Server 2016 R Services，你可以通过编辑更改服务的某些属性[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]配置文件。 此文件不能再用于更改配置。 SQL Server 配置管理器是服务配置，如服务帐户和用户数的适当方法的更改。

## <a name="debug-settings"></a>调试设置

使用快速启动板的配置文件，这可能是在有限情况下，如调试很有用，仅可以更改几个属性。 配置文件创建期间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]设置和默认情况下已为纯文本格式文件中保存`<instance path>\binn\rlauncher.config`。

你必须是运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的管理员才能对此文件进行更改。 如果你要编辑该文件，我们建议你在保存更改之前创建备份副本。

下表列出了的高级的设置[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，及其允许值。

|**设置名称**|**类型**|**说明**|
|----|----|----|
|作业\_清理\_ON\_退出|Integer |这是一项内部设置仅-不更改此值。 </br></br>指定是否为每个外部运行时会话创建的临时工作文件夹应清理完成会话后。 此设置有助于调试。 </br></br>支持的值为**0** （禁用） 或**1** （启用）。 </br></br>默认值为 1，退出时删除含义日志文件。|
|跟踪\_级别|Integer |出于调试目的配置 MSSQLLAUNCHPAD 的跟踪详细级别。 这会影响由 LOG_DIRECTORY 设置指定的路径中的跟踪文件。 </br></br>支持的值为：**1** （错误）， **2** （性能）， **3** （警告）， **4** （信息）。 </br></br>默认值为 1，这意味着只输出错误。|

所有设置采用键-值对的格式，每项设置单独占用一行。 例如，若要更改的跟踪级别，需要添加行`Default: TRACE_LEVEL=4`。

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>强制实施密码策略

如果组织中的某个策略要求定期更改密码，你可能需要强制 Launchpad 服务重新生成 Launchpad 为其辅助角色帐户维护的已加密密码。

若要启用此设置并强制密码刷新，请在 SQL Server 配置管理器中打开 Launchpad 服务的“属性”窗格，单击“高级”，然后将“重置外部用户密码”更改为“是”。     应用此更改后，将立即为所有用户帐户重新生成密码。 若要在此更改后运行外部脚本，必须重新启动 Launchpad 服务，此时它将读取新生成的密码。

若要定期重置密码，可以手动设置此标志或使用脚本。

## <a name="next-steps"></a>后续步骤

+ [可扩展性框架](../concepts/extensibility-framework.md)
+ [安全性概述](../concepts/security.md)
