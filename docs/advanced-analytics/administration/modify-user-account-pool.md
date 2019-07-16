---
title: 缩放并发执行的外部脚本的 SQL Server 机器学习服务
description: 在要扩展 SQL Server 机器学习服务的用户帐户池配置并行或并发 R 和 Python 脚本执行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: b672ce067d5d1f10754f346c77967b4e3fbe34ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963164"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>缩放并发执行的 SQL Server 机器学习服务中的外部脚本的
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在安装 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 的过程中，将创建一个新的 Windows *用户帐户池*来支持 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的任务执行。 这些辅助角色帐户的目的是隔离的不同 SQL 用户的外部脚本并发执行。

本文介绍的默认配置和容量的辅助角色帐户，以及如何更改默认配置，以在 SQL Server 机器学习服务中缩放的并发执行的外部脚本的数量。

## <a name="worker-account-group"></a>辅助角色帐户组

通过创建一个 Windows 帐户组[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]哪台计算机安装并启用了学习每个实例的安装程序。

- 在默认实例中，该组的名称为 **SQLRUserGroup**。 无论您是使用 R 或 Python，名称都是相同的。
- 在命名的实例中，默认的组名称以实例名称作为后缀：例如 **SQLRUserGroupMyInstanceName**。

用户帐户池默认包含 20 个用户帐户。 在大多数情况下，20 多个足够用来支持机器学习任务，但可以更改帐户的数目。 帐户的最大数目为 100。

- 在默认实例中，各个帐户命名为 **MSSQLSERVER01** 到 **MSSQLSERVER20**。
- 对于命名的实例，各个帐户根据实例名称命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。

如果多个实例使用机器学习，计算机将具有多个用户组。 无法在实例之间共享一个组。

> [!Note]
> 在 SQL Server 2019 **SQLRUserGroup**仅有一个成员，它现在是而不是多个辅助角色帐户的单个 SQL Server 快速启动板服务帐户。

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>辅助角色帐户数目

若要修改帐户池中的用户数目，必须按如下所述编辑 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的属性。

与每个用户帐户关联的密码是随机生成的，但在创建帐户后，你可以更改这些密码。

1. 打开 SQL Server 配置管理器并选择“SQL Server 服务”。 
2. 双击 SQL Server Launchpad 服务并停止该服务（如果正在运行）。
3.  在“服务”选项卡上，确保“启动模式”设置为“自动”。  快速启动板未运行时，无法启动外部脚本。
4.  单击“高级”选项卡，然后根据需要编辑“外部用户计数”的值。   此设置将控制多少不同的 SQL 用户可以运行外部脚本并发会话。 默认值为 20 个帐户。 用户的最大数目为 100。
5. （可选）如果组织中的策略要求定期更改密码，可将选项“重置外部用户密码”设置为“是”。   这样，便会重新生成 Launchpad 为用户帐户维护的已加密密码。 有关详细信息，请参阅[实施密码策略](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy)。
6.  重新启动 Launchpad 服务。

## <a name="managing-workloads"></a>管理工作负荷

在此池的帐户数确定多少个外部脚本会话同时可以处于活动状态。  默认情况下，会创建 20 个帐户，这意味着，20 个不同的用户可以具有活动 R 或 Python 会话一次。 如果您希望运行 20 个以上的并发脚本，您可以增加辅助角色帐户的数量。

当同一用户同时执行多个外部脚本时，所有会话运行由该用户使用同一个辅助角色帐户。 例如，单个用户可能同时运行，只要资源允许，但所有脚本都将都运行使用单个辅助角色帐户 100 不同的 R 脚本。

您可以支持的辅助角色帐户数目和任何单个用户可运行的并发会话数仅受服务器资源。 通常，在使用 R 运行时时，内存是遇到的第一个瓶颈。

可以使用 Python 或 R 脚本的资源受 SQL Server。 我们建议使用 SQL Server DMV 监视资源用量，或者查看关联 Windows 作业对象中的性能计数器，并相应地调整服务器内存用量。 如果有 SQL Server Enterprise Edition 时，你可以分配用于通过配置来运行外部脚本的资源[外部资源池](how-to-create-a-resource-pool.md)。

## <a name="see-also"></a>请参阅

有关配置容量的其他信息，请参阅以下文章：

- [R Services 的 SQL Server 配置](../../advanced-analytics/r/sql-server-configuration-r-services.md)
- [R Services 的性能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)