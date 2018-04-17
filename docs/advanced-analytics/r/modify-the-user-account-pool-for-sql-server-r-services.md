---
title: 修改用户帐户池的 SQL Server 机器学习 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 77b84e3117b0a1366f3d0b5f9d74802d938bc86b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="modify-the-user-account-pool-for-sql-server-machine-learning"></a>修改用户帐户池的 SQL Server 机器学习
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在安装 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 的过程中，将创建一个新的 Windows *用户帐户池*来支持 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的任务执行。 这些辅助帐户旨在隔离由不同的 SQL 用户的外部脚本的并发执行。

本文介绍的默认配置、 安全性和工作人员帐户，以及如何更改默认配置的容量。

**适用于：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]， [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="worker-accounts-used-for-external-script-execution"></a>用于外部脚本执行的工作帐户

此 Windows 帐户组创建的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]哪台计算机安装并启用学习每个实例的安装程序。

-   在默认实例中，该组的名称为 **SQLRUserGroup**。 无论你使用 R 和 / 或 Python，名称都是相同的。
-   在命名的实例中，默认的组名称以实例名称作为后缀：例如 **SQLRUserGroupMyInstanceName**。

用户帐户池默认包含 20 个用户帐户。 在大多数情况下，20 多个足够用来支持机器学习任务，但你可以更改的帐户的数量。 帐户的最大数目为 100。
-  在默认实例中，各个帐户命名为 **MSSQLSERVER01** 到 **MSSQLSERVER20**。
-   对于命名的实例，各个帐户根据实例名称命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。

如果多个实例使用机器学习，计算机将具有多个用户组。 无法在实例之间共享一组。

### <a name = "HowToChangeGroup"> </a>如何更改辅助帐户数

若要修改帐户池中的用户数目，必须按如下所述编辑 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的属性。

与每个用户帐户关联的密码是随机生成的，但在创建帐户后，你可以更改这些密码。

1. 打开 SQL Server 配置管理器并选择“SQL Server 服务”。
2. 双击 SQL Server Launchpad 服务并停止该服务（如果正在运行）。
3.  在“服务”选项卡上，确保“启动模式”设置为“自动”。 快速启动板未运行时，无法启动外部脚本。
4.  单击“高级”选项卡，然后根据需要编辑“外部用户计数”的值。 此设置控制如何多个不同的 SQL 用户可以运行外部脚本并发会话。 默认值为 20 的帐户。 最大用户数为 100。
5. （可选）如果组织中的策略要求定期更改密码，可将选项“重置外部用户密码”设置为“是”。 这样，便会重新生成 Launchpad 为用户帐户维护的已加密密码。 有关详细信息，请参阅[实施密码策略](#bkmk_EnforcePolicy)。
6.  重新启动快速启动板服务。

## <a name="managing-machine-learning-workloads"></a>管理机器学习工作负荷

此池中的帐户数确定多少外部脚本会话可以同时处于活动状态。  默认情况下，20 创建帐户，这意味着，20 个不同的用户可以有活动 R 或 Python 会话一次。 如果您希望运行 20 个以上的并发脚本，你可以增大辅助帐户数。

当同一用户同时执行多个外部脚本时，所有会话运行由该用户将使用相同的工作线程帐户。 例如，单个用户可能有不同，只要允许资源，但使用的单个辅助帐户运行所有脚本将同时运行的 100 R 脚本。

你可以支持的工作帐户数和可以运行任何单个用户，请的并发会话数仅受服务器资源。 通常，在使用 R 运行时时，内存是遇到的第一个瓶颈。

可以使用 Python 或 R 脚本的资源受 SQL Server。 我们建议使用 SQL Server DMV 监视资源用量，或者查看关联 Windows 作业对象中的性能计数器，并相应地调整服务器内存用量。 如果你有 SQL Server Enterprise Edition，则可以分配用于通过配置运行外部脚本的资源[外部资源池](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)。

有关管理计算机的其他信息学习任务容量，请参阅以下文章：

- [R Services 的 SQL Server 配置](../../advanced-analytics/r/sql-server-configuration-r-services.md)
-  [对于 R 服务的性能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)

## <a name="security"></a>Security

每个用户组都与特定实例上的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务相关联，并且无法支持其他实例上运行的 R 作业。

对于每个辅助角色帐户，当会话处于活动状态时，将创建一个临时文件夹来存储脚本对象、中间结果，以及执行 R 脚本期间 R 和 SQL Server 所用的其他信息。 这些工作文件位于 ExtensibilityData 文件夹中，仅限管理员访问，脚本执行完成后，将由 SQL Server 清除。 

有关详细信息，请参阅[安全概述](../../advanced-analytics/r-services/security-overview-sql-server-r.md)。

### <a name="bkmk_EnforcePolicy"></a>实施密码策略

如果组织中的某个策略要求定期更改密码，你可能需要强制 Launchpad 服务重新生成 Launchpad 为其辅助角色帐户维护的已加密密码。  

若要启用此设置并强制密码刷新，请在 SQL Server 配置管理器中打开 Launchpad 服务的“属性”窗格，单击“高级”，然后将“重置外部用户密码”更改为“是”。 应用此更改后，将立即为所有用户帐户重新生成密码。 若要在应用此更改后使用 R 脚本，必须重新启动 Launchpad 服务，随后它将会读取新生成的密码。 

若要定期重置密码，可以手动设置此标志或使用脚本。

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>支持远程计算上下文所需的其他权限

默认情况下，R 辅助角色帐户组对它关联到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例**没有**登录权限。 如果任何 R 用户从远程客户端连接到 SQL Server 来运行 R 脚本，或者脚本使用 ODBC 来获取其他数据，则这种限制可能会造成问题。 

为了确保支持这些方案，数据库管理员必须为 R 辅助角色帐户组提供相应的权限，使其能够登录到要运行 R 脚本的 SQL Server 实例（“连接到”权限）。 这称为*默示身份验证*，并启用 SQL Server 以运行 R 脚本使用远程用户的凭据。

> [!NOTE]
> 如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制，因为 SQL 登录凭据将从 R 客户端显式传递到 SQL Server 实例，再到 ODBC。


### <a name="how-to-enable-implied-authentication"></a>如何启用隐含的身份验证

1. 以管理员身份在将运行 R 或 Python 代码的实例上打开 SQL Server Management Studio。

2. 运行以下脚本。 如果更改了默认值、计算机和实例名称，请务必编辑用户组名称。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ````

