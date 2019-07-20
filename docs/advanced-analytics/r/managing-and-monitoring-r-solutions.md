---
title: 管理和集成机器学习工作负荷
description: 作为 SQL Server DBA, 请查看用于在数据库引擎实例上部署机器学习 R 和 Python 子系统的管理任务。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: fab91e142fad3bcb1ce23816d6705f7a7d208851
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345316"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>管理和集成 SQL Server 上的机器学习工作负荷
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文适用于负责在支持多个工作负荷的服务器资产上部署高效数据科学基础结构的 SQL Server 数据库管理员。 它使管理问题空间与在 SQL Server 上管理 R 和 Python 代码执行的相关。 

## <a name="what-is-feature-integration"></a>什么是功能集成

R 和 Python 机器学习通过[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)作为数据库引擎实例的扩展提供。 集成主要通过安全层和数据定义语言, 总结如下:

+ 存储过程具备接受 R 和 Python 代码作为输入参数的功能。 开发人员和数据科学家可以使用[系统存储过程](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017)或创建包装其代码的自定义过程。
+ T-sql 函数 (即[预测](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)), 可以使用以前训练的数据模型。 此功能通过 T-sql 提供。 因此, 它可以在未安装机器学习扩展的系统上调用。
+ 现有数据库登录名和基于角色的权限覆盖了使用相同数据的用户调用的脚本。 一般规则是, 如果用户无法通过查询访问数据, 则他们不能通过脚本访问数据。

## <a name="feature-availability"></a>功能可用性

通过连续的步骤, 可以使用 R 和 Python 集成。 第一种设置是在将[**机器学习服务**功能添加](../install/sql-machine-learning-services-windows-install.md)到数据库引擎实例时进行设置。 在后续步骤中, 必须在数据库引擎实例上启用外部脚本 (默认情况下处于关闭状态)。

此时, 只有数据库管理员具有创建和运行外部脚本的完全权限、添加或删除包以及创建存储过程和其他对象。

所有其他用户必须被授予 "执行任何外部脚本" 权限。 其他[标准数据库权限](../security/user-permission.md)确定用户是否可以创建对象, 运行脚本, 使用序列化和定型模型等。 

## <a name="resource-allocation"></a>资源分配

调用外部处理的存储过程和 T-sql 查询使用可用于默认资源池的资源。 作为默认配置的一部分, 在使用外部进程 (如 R 和 Python 会话) 时, 最多允许主机系统上的总内存的 20%。 

如果要重新调整资源的状态, 可以修改默认池, 并对在该系统上运行的机器学习工作负荷产生相应影响。

另一种方法是创建自定义外部资源池, 以便捕获特定时间间隔内发生的特定程序、主机或活动的会话。 有关详细信息, 请参阅[资源调控: 修改 R 和 Python 执行的资源级别](../administration/resource-governance.md)和[如何创建资源池](../administration/how-to-create-a-resource-pool.md)以获取分步说明。

## <a name="isolation-and-containment"></a>隔离和包含

处理体系结构旨在隔离核心引擎处理中的外部脚本。 R 和 Python 脚本在本地辅助角色帐户下作为单独的进程运行。 在任务管理器中, 可以监视 R 和 Python 进程, 该进程在低特权本地用户帐户下执行, 这与 SQL Server 服务帐户不同。 

在单独的低特权帐户中运行 R 和 Python 进程具有以下优势:

+ 从 R 和 Python 会话中隔离核心引擎进程可以终止 R 或 Python 进程, 而不会影响核心数据库操作。 

+ 减少主计算机上的外部脚本运行时进程的特权。

最小特权帐户是在安装过程中创建的, 并放置在名为**SQLRUserGroup**的 Windows*用户帐户池中*。 默认情况下, 此组有权在 SQL Server 的 R 和 Python 的 program 文件夹中使用可执行文件、库和内置数据集。 

作为 DBA, 你可以使用 SQL Server data security 来指定有权执行脚本的人员, 并使用通过 T-sql 查询控制访问权限的同一安全角色来管理作业中使用的数据。 作为系统管理员, 你可以通过创建 Acl 来显式拒绝**SQLRUserGroup**对本地服务器上敏感数据的访问。

>[!NOTE]
> 默认情况下, **SQLRUserGroup**没有 SQL Server 本身中的登录名或权限。 如果工作人员帐户需要登录才能进行数据访问, 则必须自行创建。 在用户标识是 Windows 用户并且连接字符串指定了可信用户的情况下, 专门调用用于创建登录名的方案是为了支持对数据库引擎实例上的数据或操作执行请求。 有关详细信息, 请参阅[Add SQLRUserGroup as a database user](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)。

## <a name="disable-script-execution"></a>禁用脚本执行

如果脚本失控, 你可以禁用所有脚本执行, 并反转之前执行的步骤, 以首先启用外部脚本执行。

1. 在 SQL Server Management Studio 或其他查询工具中, 运行此命令以`external scripts enabled`将设置为0或 FALSE。

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. 重新启动数据库引擎服务。

解决问题后, 如果想要恢复数据库引擎实例上的 R 和 Python 脚本支持, 请记得在实例上重新启用脚本执行。 有关详细信息, 请参阅[启用脚本执行](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>扩展功能

数据科学通常为包部署和管理提供了新的要求。 对于数据科学家而言, 一般的做法是在自定义解决方案中利用开源和第三方包。 其中一些包将依赖于其他包, 在这种情况下, 可能需要评估和安装多个包才能达到目标。

作为负责服务器资产的 DBA, 将任意 R 和 Python 包部署到生产服务器上都表示不熟悉的挑战。 在添加包之前, 你应该评估外部包提供的功能是否确实是必需的, 并且在 SQL Server 安装程序安装的内置[R 语言](r-libraries-and-data-types.md)和[Python 库](../python/python-libraries-and-data-types.md)中没有等效项。 

作为服务器包安装的替代方法, 数据科学家可以[在外部工作站上构建和运行解决方案](../r/set-up-a-data-science-client.md), 从 SQL Server 检索数据, 但在工作站上 (而不是在服务器上) 执行所有分析自动. 

如果你随后确定外部库函数是必需的, 并且不会对服务器操作或数据整体造成风险, 则可以从多种方法中选择添加包。 在大多数情况下, 需要管理员权限才能将包添加到 SQL Server。 若要了解详细信息, 请参阅[在 SQL Server 中安装 Python 包](../python/install-additional-python-packages-on-sql-server.md)并[在 SQL Server 中安装 R 包](install-additional-r-packages-on-sql-server.md)。

> [!NOTE]
> 对于 R 包, 如果使用其他方法, 则不会特别要求服务器管理员权限。 有关详细信息, 请参阅[在 SQL Server 中安装 R 包](install-additional-r-packages-on-sql-server.md)。

## <a name="monitoring-script-execution"></a>监视脚本执行

中[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]运行的 R 和 Python 脚本[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]由接口启动。 但是, 快速启动板不是资源管理或单独监视, 因为它是 Microsoft 提供的一种安全服务, 它可相应地管理资源。

在快速启动板服务下运行的外部脚本使用[Windows 作业对象](/windows/desktop/ProcThread/job-objects)进行管理。 使用作业对象可将进程组作为一个单元进行管理。 每个作业对象都是分层的，可控制与其关联的所有进程的属性。 针对某个作业对象执行的操作会影响与该作业对象关联的所有进程。

因此，如果需要终止与某个对象关联的一个作业，请注意所有相关的进程也会终止。 如果运行一个已分配到 Windows 作业对象的 R 脚本，并且该脚本运行一个必须终止的相关 ODBC 作业，则父 R 脚本进程也会终止。

如果启动使用并行处理的外部脚本, 则单个 Windows 作业对象会管理所有并行子进程。

若要确定进程是否在作业中运行，请使用 `IsProcessInJob` 函数。

## <a name="next-steps"></a>后续步骤

+ 查看[扩展性体系结构](../concepts/extensibility-framework.md)和[安全性](../concepts/security.md)的概念和组件, 了解更多背景知识。

+ 作为功能安装的一部分, 你可能已经熟悉最终用户数据访问控制, 但如果没有, 请参阅[向用户授予 SQL Server 机器学习的权限](../security/user-permission.md)。 

+ 了解如何调整计算密集型机器学习工作负荷的系统资源。 有关详细信息, 请参阅[如何创建资源池](../administration/how-to-create-a-resource-pool.md)。
