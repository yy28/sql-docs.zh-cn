---
title: SQL Server 中的 R 语言支持的体系结构概述 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3784fe62669b3f6d29e94bea799e19f9eadad5f0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="architecture-overview-for-r-in-sql-server"></a>SQL Server 中的 R 的体系结构概述
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本部分概述了 SQL Server 2016 R services 和 SQL Server 自 2017 年 1 机器学习服务的体系结构。

可扩展性体系结构的体系结构是相同或非常类似于 SQL Server 2016 和 SQL Server 自 2017 年 1 版本中，以及类似还为 R 和 Python。 但是，若要简化讨论，本文讨论仅是 R 组件，包括 SQL Server 数据库引擎，以支持外部脚本执行、 安全、 R 库和与开放源代码。 互操作性中添加新组件

每个部分的链接中提供其他详细信息。

## <a name="r-interoperability"></a>R 互操作性

SQL Server 2016 R Services 和 SQL Server 自 2017 年 1 机器学习 Services （数据库中） 安装 R，以及支持分布式和/或并行处理的包由 Microsoft 提供的开源的分发。

体系结构的设计目的的这样在单独的进程中运行从 SQL Server 的外部使用 R 的脚本。 R 的当前用户应该能够通过相对较小的修改移植其 R 代码，并在 T-SQL 中执行。

若要缩放你的解决方案，或使用并行处理，我们建议你使用[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)包或[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)包。 如果不使用这些库提供的分布式计算功能，你仍可以通过在 SQL Server 的上下文中运行 R 代码获取一些性能改进。

有关外部脚本已安装的组件或使用 R 的 SQL Server 的交互的详细信息，请参阅[R 互操作性](../../advanced-analytics/r/r-interoperability-in-sql-server.md)

## <a name="components-to-support-r-integration"></a>组件来支持 R 集成

在 SQL Server 自 2017 年中，SQL Server 2016 中引入的 extensibility framework 将继续运行。 SQL server 使用的可扩展性组件用于启动 R、 R 和数据库引擎，之间传递数据并协调 R 作业所需的并行任务的外部运行时。

这些其他组件的角色是提高数据 exchange 速度和压缩，同时提供用于在运行外部脚本的一个安全、 高性能的平台。

有关支持 R，如的组件的详细说明[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]和 RLauncher，请参阅[新组件](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)。

## <a name="security"></a>Security

使用机器学习服务或 SQL Server R Services 的 R 代码运行时，所有 R 脚本都执行外部 SQL Server 过程中，以提供安全和更高版本的可管理性。 这种隔离的进程如此无论你是否作为存储过程的一部分运行 R 脚本或从远程计算机连接到 SQL Server 计算机作业并开始使用服务器作为计算上下文的作业。

SQL Server 截获所有作业请求、 任务和使用 Windows 作业对象，其数据保护和通过使用 SQL Server 用户帐户和数据库角色的数据保持安全。

通过强制在表、 数据库和实例级别的 SQL Server 安全情况下，数据保留在法规遵从性边界内。 数据库管理员可以控制谁有能够运行 R 作业以及谁可以安装或共享的 R 程序包的功能。 管理员还可以监视由远程或本地用户的 R 脚本的使用和监视和管理所占用的资源。

## <a name="next-steps"></a>后续步骤

[支持 R 集成的组件](new-components-in-sql-server-to-support-r.md)

[R 互操作性](r-interoperability-in-sql-server.md)

[安全性概述](security-overview-sql-server-r.md)
