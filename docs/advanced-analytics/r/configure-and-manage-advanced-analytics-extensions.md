---
title: SQL Server 机器学习服务的高级的配置 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8384773f6db4c0ced2fc68e52cd78100c98c52fd
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395639"
---
# <a name="advanced-configuration-options-for-sql-server-machine-learning-services"></a>SQL Server 机器学习服务的高级的配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍所做的更改可以设置完成后，若要修改的外部脚本运行时和 SQL Server 中机器学习与关联的其他服务的配置。

**适用于：** SQL Server 2016 R Services、 SQL Server 2017 机器学习服务

##  <a name="bkmk_Provisioning"></a> 预配其他用户帐户，机器学习

外部脚本以处理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]低特权本地用户帐户的上下文中运行。 在单个低特权帐户中运行这些进程具有以下优势：

+ 在减少特权的外部脚本运行时进程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机
+ 如 R 或 Python 的外部运行时的会话之间提供隔离。

作为安装过程中，新的 Windows 的一部分*用户帐户池*创建，其中包含正在运行的外部运行时进程，R 或 Python 等所需的本地用户帐户。 可以根据需要以支持机器学习任务修改用户的数。 

此外，数据库管理员必须授予此组的权限连接到已启用机器学习的任何实例。 有关详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。

对 protext 敏感资源上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以定义此组的访问控制列表 (ACL)。 通过指定组将被拒绝访问的资源，可以由外部进程，例如 R 或 Python 运行时阻止访问。

+ 用户帐户池链接到一个特定的实例。 已在哪台计算机启用了学习每个实例需要一个单独的池的辅助角色帐户。 帐户不能在各个实例之间共享。

+ 池中的用户帐户名采用 SQLInstanceName*nn*格式。 例如，如果对机器学习使用默认实例，用户帐户池支持帐户名称，如 MSSQLSERVER01、 MSSQLSERVER02，等等。

+ 用户帐户池的大小是静态的，默认值为 20。 可以同时启动的外部运行时会话数受此用户帐户池的大小。 若要更改此限制，管理员应使用 SQL Server 配置管理器。

有关如何更改用户帐户池的详细信息，请参阅[修改 SQL Server 机器学习服务的用户帐户池](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)。

##  <a name="bkmk_ManagingMemory"></a> 管理外部脚本进程所使用的内存

默认情况下，机器学习的外部脚本运行时仅限于不超过 20%的总计算机内存。 这取决于您的系统，但一般情况下，你可能会发现此限制不足以严重的机器学习任务，例如为模型定型或预测在很多行数据。 

若要支持机器学习，管理员可以增加此限制。 执行此操作时，可能需要减少保留的内存量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或其他服务。 此外应考虑使用资源调控器来定义外部资源池或池，以便你可以分配给 R 或 Python 的作业的特定资源池。

有关详细信息，请参阅[机器学习的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)。


## <a name="bkmk_Launchpad"></a>修改快速启动板服务帐户

单独[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]为每个实例在其已配置机器学习服务创建服务。

默认情况下，启动板配置为使用帐户 NT Service\MSSQLLaunchpad 运行，该帐户预配有运行 R 脚本所需的所有权限。 但是，如果更改此帐户，快速启动板可能无法启动或访问应在何处运行外部脚本的 SQL Server 实例。

如果你修改了服务帐户，请务必使用**本地安全策略**应用程序并更新每个服务帐户的权限以包括以下权限：

+ 调整进程的内存配额 (SeIncreaseQuotaPrivilege)
+ 跳过遍历检查 (SeChangeNotifyPrivilege)
+ 以服务身份登录 (SeServiceLogonRight)
+ 替换进程级别标记 (SeAssignPrimaryTokenPrivilege)

若要深入了解运行 SQL Server 服务所需的权限，请参阅[配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。

##  <a name="bkmk_ChangingConfig"></a> 更改高级的服务选项

在早期版本的 SQL Server 2016 R Services，你可以通过编辑更改服务的某些属性[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]配置文件。 

但是，此文件不能再用于更改配置。 我们建议你使用 SQL Server 配置管理器对服务配置，如服务帐户和用户数的效果更改。

**若要修改快速启动板配置**

1. 打开 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)。 
2. 右键单击 SQL Server 快速启动板，然后选择**属性**。

    + 若要更改服务帐户，请单击**Log On**选项卡。

    + 若要增加的用户数，请单击**高级**选项卡。


**若要修改调试设置**

使用快速启动板的配置文件，这可能是在有限情况下，如调试很有用，仅可以更改几个属性。 配置文件创建期间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]设置和默认情况下保存为纯文本格式文件的以下位置： `<instance path>\binn\rlauncher.config`

你必须是运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的管理员才能对此文件进行更改。 如果你要编辑该文件，我们建议你在保存更改之前创建备份副本。

下表列出了的高级的设置[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，及其允许值。 

|**设置名称**|**类型**|**Description**|
|----|----|----|
|作业\_清理\_ON\_退出|Integer |这是一项内部设置仅 – 请不要更改此值。 </br></br>指定是否为每个外部运行时会话创建的临时工作文件夹应清理完成会话后。 此设置有助于调试。 </br></br>支持的值为**0** （禁用） 或**1** （启用）。 </br></br>默认值为 1，退出时删除含义日志文件。|
|跟踪\_级别|Integer |出于调试目的配置 MSSQLLAUNCHPAD 的跟踪详细级别。 这会影响由 LOG_DIRECTORY 设置指定的路径中的跟踪文件。 </br></br>支持的值为： **1** （错误）， **2** （性能） **3** （警告）， **4** （信息）。 </br></br>默认值为 1，这意味着仅输出警告。|

所有设置采用键-值对的格式，每项设置单独占用一行。 例如，若要更改的跟踪级别，需要添加行`Default: TRACE_LEVEL=4`。

## <a name="see-also"></a>请参阅

[安全注意事项](security-considerations-for-the-r-runtime-in-sql-server.md)
