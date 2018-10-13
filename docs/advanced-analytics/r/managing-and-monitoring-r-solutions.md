---
title: 管理和集成在 SQL Server 中的机器学习工作负荷 |Microsoft Docs
description: 为 SQL Server DBA，查看用于部署机器学习 R 和 Python 的子系统，数据库引擎实例上的管理任务。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c921b89dc3f6928ccbfc3f9fc727015dadc05b7b
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169077"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>管理和集成 SQL Server 上的机器学习工作负荷
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文适用于 SQL Server 数据库管理员负责部署高效的数据科学基础结构上支持多个工作负荷的服务器资产。 帧与 R 的管理相关的管理问题空间和 Python 代码在 SQL Server 上的执行。 

## <a name="what-is-feature-integration"></a>什么是功能集成

提供 R 和 Python 机器学习[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)作为数据库引擎实例的扩展。 集成是主要通过安全层和数据定义语言，总结如下：

+ 存储的过程都配备了能够接受 R 和 Python 代码作为输入的参数。 可以使用开发人员和数据科学家[系统存储过程](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017)或创建包装其代码的自定义过程。
+ T-SQL 函数 (即[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql))，可使用先前定型的数据模型。 此功能是可通过 T-SQL。 在这种情况下，它可以调用不专门具有机器学习安装扩展的系统上。
+ 现有的数据库登录名和基于角色的权限包括利用相同的数据的用户调用脚本。 作为一般规则，如果用户无法访问数据，通过一个查询，但不能访问通过脚本或者。

## <a name="feature-availability"></a>功能可用性

R 和 Python 集成变得可通过一系列步骤。 第一个参数是安装程序，当您[包括或添加**机器学习服务**](../install/sql-machine-learning-services-windows-install.md)到数据库引擎实例的功能。 作为后续步骤中，必须启用外部脚本 （其默认处于关闭状态） 在数据库引擎实例上。

在此情况下，只有数据库管理员具有完全权限创建和运行外部脚本、 添加或删除包，并创建存储的过程和其他对象。

必须为所有其他用户授予 EXECUTE ANY EXTERNAL SCRIPT 权限。 其他[标准数据库权限](../security/user-permission.md)确定用户是否可以创建对象、 运行脚本，使用序列化和训练模型和等等。 

## <a name="resource-allocation"></a>资源分配

存储的过程和调用外部处理的 T-SQL 查询到默认资源池使用可用的资源。 作为默认配置的一部分，外部的进程，如 R 和 Python 会话允许最多 20%的总内存的主机系统上。 

如果你想要重新调整资源，可以修改默认池，使用相应运行该系统上的机器学习工作负荷的影响。

另一种方法是创建一个自定义的外部资源池来捕获源自特定程序、 主机或发生在特定时间间隔期间活动的会话。 有关详细信息，请参阅[若要修改的 R 和 Python 执行资源级别的资源调控](../administration/resource-governance.md)并[如何创建资源池](../administration/how-to-create-a-resource-pool.md)有关分步说明。

## <a name="isolation-and-containment"></a>隔离和包容

处理体系结构设计，以隔离来自核心引擎处理的外部脚本。 R 和 Python 脚本作为单独的进程，在本地的辅助角色帐户下运行。 在任务管理器中，你可以监视 R 和 Python 进程执行低特权本地用户帐户，不同于 SQL Server 服务帐户。 

在单个低特权帐户中运行 R 和 Python 进程具有以下优势：

+ 将 R 和 Python 会话而不会影响核心数据库操作，可以终止 R 或 Python 进程中的核心引擎进程中隔离出来。 

+ 减少了在主计算机上的外部脚本运行时进程的权限。

最小特权帐户将在安装期间创建并在 Windows 中放置*用户帐户池*称为**SQLRUserGroup**。 默认情况下，此组具有可执行文件、 库和内置的数据集使用对 R 和 Python 在 SQL Server 中的程序文件夹的权限。 

作为数据库管理员，可以使用 SQL Server 数据安全性来指定哪些人拥有权限来执行脚本，并在作业中使用的数据进行管理下的相同的安全角色来控制访问通过 T-SQL 查询。 作为系统管理员，你可以显式拒绝**SQLRUserGroup**对通过创建 Acl 在本地服务器上的敏感数据的访问。

>[!NOTE]
> 默认情况下**SQLRUserGroup**中 SQL Server 本身不具有登录名或权限。 如果数据访问辅助角色帐户需要一个登录名，您必须自行创建它。 专门调用创建一个登录名的方案是在执行中，数据或对数据库引擎实例中的操作支持来自脚本的请求时的用户标识是 Windows 用户和连接字符串指定受信任的用户。 有关详细信息，请参阅[作为数据库用户添加 SQLRUserGroup](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)。

## <a name="disable-script-execution"></a>禁用脚本执行

出现失控脚本时可以禁用所有脚本执行，撤消以前执行第一个位置中启用外部脚本执行的步骤。

1. 在 SQL Server Management Studio 或其他查询工具中，运行以下命令来设置`external scripts enabled`为 0 或 FALSE。

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. 重新启动数据库引擎服务。

一旦解决此问题，请记住重新启用脚本执行的实例上，如果你想要恢复 R 和 Python 脚本支持数据库引擎实例上。 有关详细信息，请参阅[启用脚本执行](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>扩展功能

数据科学通常引入了新的包部署和管理的要求。 对于数据科学家，它是利用开源和第三方包的自定义解决方案中常见的做法。 一些这些包将其他包上具有依赖项，这种情况下，可能需要评估和安装多个包来访问您的目标。

负责服务器资产 DBA，作为部署到生产服务器上的任意 R 和 Python 包表示一个不熟悉的挑战。 然后再添加包，您应评估外部包提供的功能是否真正需要，使用内置中没有等效项[R 语言](r-libraries-and-data-types.md)并[Python 库](../python/python-libraries-and-data-types.md)安装SQL Server 安装程序。 

Server 包安装的替代方法，为数据科学家可能能够[生成并运行解决方案外部的工作站上](../r/set-up-a-data-science-client.md)，从 SQL Server 中检索数据，但使用所有分析执行本地工作站上而不是服务器本身上。 

如果您随后确定外部库函数有必要，不会造成服务器操作或作为一个整体的数据风险，您可以选择从多个方法添加包。 在大多数情况下，都需要将包添加到 SQL Server 管理员权限。 若要了解详细信息，请参阅[SQL Server 中的安装 Python 包](../python/install-additional-python-packages-on-sql-server.md)并[SQL Server 中的安装 R 包](install-additional-r-packages-on-sql-server.md)。

> [!NOTE]
> 获取 R 包，服务器管理员权限不专门需要针对包安装如果您使用替代方法。 请参阅[SQL Server 中的安装 R 包](install-additional-r-packages-on-sql-server.md)有关详细信息。

## <a name="next-steps"></a>后续步骤

+ 查看相关概念和组件[可扩展性体系结构](../concepts/extensibility-framework.md)并[安全](../concepts/security.md)的更多背景。

+ 作为功能安装的一部分，您可能已经很熟悉与最终用户数据的访问控制，但如果没有，请参阅[授予对 SQL Server 机器学习的用户权限](../security/user-permission.md)有关详细信息。 

+ 了解如何调整需要进行大量计算的机器学习工作负荷的系统资源。 有关详细信息，请参阅[如何创建资源池](../administration/how-to-create-a-resource-pool.md)。
