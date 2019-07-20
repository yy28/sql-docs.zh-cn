---
title: 扩展外部脚本的并发执行
description: 在用户帐户池中配置并行或并发 R 和 Python 脚本执行以缩放 SQL Server 机器学习服务。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e44137b539b24bc6cdb8fc55f2df2877c19babe2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344028"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>在 SQL Server 机器学习服务中扩展外部脚本的并发执行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在安装 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 的过程中，将创建一个新的 Windows *用户帐户池*来支持 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的任务执行。 这些辅助角色帐户的用途是将不同 SQL 用户的外部脚本并发执行隔离开来。

本文介绍辅助角色帐户的默认配置和容量, 以及如何更改默认配置, 以扩展 SQL Server 机器学习服务中外部脚本的并发执行数。

## <a name="worker-account-group"></a>工作线程帐户组

对于安装和启用了机器学习[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个实例, 将为安装程序创建一个 Windows 帐户组。

- 在默认实例中，该组的名称为 **SQLRUserGroup**。 无论你使用的是 R 还是 Python, 名称都是相同的。
- 在命名的实例中，默认的组名称以实例名称作为后缀：例如 **SQLRUserGroupMyInstanceName**。

用户帐户池默认包含 20 个用户帐户。 在大多数情况下, 20 是足以支持机器学习任务的, 但您可以更改帐户的数量。 最大帐户数为100。

- 在默认实例中，各个帐户命名为 **MSSQLSERVER01** 到 **MSSQLSERVER20**。
- 对于命名的实例，各个帐户根据实例名称命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。

如果有多个实例使用机器学习, 则计算机将有多个用户组。 不能跨实例共享组。

> [!Note]
> 在 SQL Server 2019 中, **SQLRUserGroup**只具有一个现在为单一 SQL Server Launchpad 服务帐户而不是多个辅助角色帐户的成员。

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>辅助角色帐户的数目

若要修改帐户池中的用户数目，必须按如下所述编辑 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的属性。

与每个用户帐户关联的密码是随机生成的，但在创建帐户后，你可以更改这些密码。

1. 打开 SQL Server 配置管理器并选择“SQL Server 服务”。 
2. 双击 SQL Server Launchpad 服务并停止该服务（如果正在运行）。
3.  在“服务”选项卡上，确保“启动模式”设置为“自动”。  当启动板未运行时, 无法启动外部脚本。
4.  单击“高级”选项卡，然后根据需要编辑“外部用户计数”的值。   此设置控制有多少不同的 SQL 用户可同时运行外部脚本会话。 默认值为20个帐户。 最大用户数为100。
5. （可选）如果组织中的策略要求定期更改密码，可将选项“重置外部用户密码”设置为“是”。   这样，便会重新生成 Launchpad 为用户帐户维护的已加密密码。 有关详细信息，请参阅[实施密码策略](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy)。
6.  重新启动启动板服务。

## <a name="managing-workloads"></a>管理工作负荷

此池中的帐户数目决定了可以同时处于活动状态的外部脚本会话数。  默认情况下, 会创建20个帐户, 这意味着20个不同的用户可同时拥有活动 R 或 Python 会话。 如果你希望运行超过20个并发脚本, 则可以增加辅助角色帐户的数目。

当同一用户同时执行多个外部脚本时, 该用户运行的所有会话都使用同一辅助角色帐户。 例如, 只要资源允许, 单个用户可能会有100个不同的 R 脚本同时运行, 但所有脚本都将使用单个辅助角色帐户运行。

您可以支持的辅助角色帐户的数目以及任何单个用户可以运行的并发会话数仅受服务器资源的限制。 通常，在使用 R 运行时时，内存是遇到的第一个瓶颈。

Python 或 R 脚本可以使用的资源由 SQL Server 控制。 我们建议使用 SQL Server DMV 监视资源用量，或者查看关联 Windows 作业对象中的性能计数器，并相应地调整服务器内存用量。 如果有 SQL Server Enterprise Edition, 则可以通过配置[外部资源池](how-to-create-a-resource-pool.md)来分配用于运行外部脚本的资源。

## <a name="see-also"></a>请参阅

有关配置容量的其他信息, 请参阅以下文章:

- [R Services 的 SQL Server 配置](../../advanced-analytics/r/sql-server-configuration-r-services.md)
- [R Services 的性能案例研究](../../advanced-analytics/r/performance-case-study-r-services.md)