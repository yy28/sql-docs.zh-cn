---
title: SQL Server 快速启动板服务帐户配置 |Microsoft Docs
description: 如何修改用于 SQL Server 上的外部脚本执行的 SQL Server 快速启动板服务帐户。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0afdb02c578de92bc91c5f47e973148136ebd919
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892851"
---
# <a name="sql-server-launchpad-service-configuration"></a>SQL Server 快速启动板服务配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

单独[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]为数据库引擎实例已向其添加 SQL Server 机器学习 （R 或 Python） 集成创建服务。

## <a name="service-account-configuration"></a>服务帐户配置

默认情况下，SQL Server 快速启动板配置下运行**NT Service\MSSQLLaunchpad**，其中预配了所有必需的权限来运行外部脚本。 最小化此帐户的权限可能会导致未能启动或访问 SQL Server 实例应在何处运行外部脚本的快速启动板。

下面列出了为此帐户所需的权限。 如果您修改的服务帐户，请务必使用**本地安全策略**应用程序以包括这些权限：

+ 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
+ 跳过遍历检查 (SeChangeNotifyPrivilege)
+ 以服务身份登录 (SeServiceLogonRight)
+ 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

若要深入了解运行 SQL Server 服务所需的权限，请参阅[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>配置属性

1. 打开 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。 

2. 右键单击 SQL Server 快速启动板，然后选择**属性**。

    + 若要更改服务帐户，请单击**Log On**选项卡。

    + 若要增加的用户数，请单击**高级**选项卡。

> [!Note]
> 在早期版本的 SQL Server 2016 R Services，你可以通过编辑更改服务的某些属性[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]配置文件。 此文件不能再用于更改配置。 SQL Server 配置管理器是服务配置，如服务帐户和用户数的适当方法的更改。

#### <a name="debug-settings"></a>调试设置

使用快速启动板的配置文件，这可能是在有限情况下，如调试很有用，仅可以更改几个属性。 配置文件创建期间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]设置和默认情况下保存为纯文本格式文件的以下位置： `<instance path>\binn\rlauncher.config`

你必须是运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的管理员才能对此文件进行更改。 如果你要编辑该文件，我们建议你在保存更改之前创建备份副本。

下表列出了的高级的设置[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，及其允许值。 

|**设置名称**|**类型**|**Description**|
|----|----|----|
|作业\_清理\_ON\_退出|Integer |这是一项内部设置仅 – 请不要更改此值。 </br></br>指定是否为每个外部运行时会话创建的临时工作文件夹应清理完成会话后。 此设置有助于调试。 </br></br>支持的值为**0** （禁用） 或**1** （启用）。 </br></br>默认值为 1，退出时删除含义日志文件。|
|跟踪\_级别|Integer |出于调试目的配置 MSSQLLAUNCHPAD 的跟踪详细级别。 这会影响由 LOG_DIRECTORY 设置指定的路径中的跟踪文件。 </br></br>支持的值为： **1** （错误）， **2** （性能） **3** （警告）， **4** （信息）。 </br></br>默认值为 1，这意味着仅输出警告。|

所有设置采用键-值对的格式，每项设置单独占用一行。 例如，若要更改的跟踪级别，需要添加行`Default: TRACE_LEVEL=4`。

## <a name="see-also"></a>另请参阅

[可扩展性框架](../concepts/extensibility-framework.md)
