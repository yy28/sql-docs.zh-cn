---
title: "资源调控 for Python |Microsoft 文档"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1fff94725d1e564b4fe9eb286ea6bf1e390a3179
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="resource-governance-for-python"></a>Python 的资源调控

因为通过启用 Python 的相同扩展性体系结构，为 SQL Server 2016 中的 R 语言实现的你可以使用现有工具 SQL Server 中例如资源调控器、 Dmv，和扩展的事件监视其执行的 PythonSQL Server 中的脚本。

资源调控具体而言非常重要，因为分析大量在生产环境中的数据可以税务甚至高级的硬件。  若要防止数据在数据库外移到不可能托管或审核的计算机，请务必数据库管理员为高级的分析操作分配足够的资源。

本部分提供有关如何管理所使用的 Python 运行时资源的信息和的 Python 资源监视器使用脚本中执行的作业[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。

> [!NOTE]
> Python 支持是 SQL Server 自 2017 年中的新功能，并在预发行版。 有关详细信息很快查看。
> 一般情况下，你可以监视任何外部脚本，包括运行 Python，使用相同的 SQL Server 2016 中的 R 脚本的资源调控为提供的框架。

## <a name="what-is-resource-governance"></a>什么是资源调控？

资源调控旨在识别和防范数据库服务器环境中的常见问题。这种环境通常包含多个要支持和平衡的依赖应用程序与服务。 对于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，资源调控涉及到以下任务：  

+ **标识使用过多的服务器资源的脚本**。 管理员需要能够终止或限制消耗过多资源的作业。

+ **缓解不可预测的工作负荷**。 如果在服务器上同时运行多个 Python 作业和作业不是相互隔离的通过使用资源池，生成的资源争用无法威胁完成的工作负荷或导致不可预测的性能。

+ **设置优先级工作负荷**。 管理员或架构师需要能够指定必须优先处理的工作负荷，或者保证在出现资源争用时能够完成某些工作负荷。

你可以使用[资源调控器](../../relational-databases/resource-governor/resource-governor.md)来管理的外部运行时使用的资源。 这包括终端但执行使用 SQL Server 计算机作为计算上下文从远程启动的 Python 脚本。

> [!NOTE] 
> 资源调控器是 Enterprise Edition 中推出。

## <a name="how-to-use-resource-governor-to-manage-python-execution"></a>如何使用资源调控器来管理 Python 执行

一般情况下，管理资源分配给任何外部脚本作业，通过创建*外部资源池*并分配到池的工作负荷。 外部资源池是一种新 SQL Server 2016，以帮助管理 R 运行时以及外部数据库引擎的其他进程中引入的资源池。 它可以用于监视从 SQL Server 自 2017 年开始的 Python 作业。

有三种类型的默认资源池：

+ *内部池*表示 SQL Server 本身使用的、不可更改或限制的资源。
+ *默认池*是预定义的用户池，可用于修改整个服务器的资源用量。 还可以定义属于此池的用户组，以管理对资源的访问。
+ *默认外部池*是外部资源的预定义用户池。 此外，可以创建新的外部资源池，并定义属于此池的用户组。

还可以创建*用户定义的资源池*将资源分配到数据库引擎或其他应用程序，创建*用户定义的外部资源池*来管理 R 和其他外部进程。

有关术语和一般概念的全面介绍，请参阅[资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。

## <a name="resource-management-using-resource-governor"></a>使用资源调控器进行资源管理

如果你不熟悉资源调控器，请参阅以下主题，获取有关如何修改实例默认资源和新建外部资源池的快速演练：[如何为 R 创建资源池](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)

你可以使用*外部资源池*机制来管理使用以下支持可执行文件的资源：

+ Python35.exe 调用从 SQL Server 或 SQL Server 作为远程计算上下文使用的远程管理调用时
+ BxlServer.exe 和附属进程
+ 通过快速启动板，如 PythonLauncher.dll 启动的启动程序

> [!NOTE]
> 不支持通过使用资源调控器的快速启动板服务的直接管理。 这是因为 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是一个受信任的服务，在设计上只能托管 Microsoft 提供的启动器。 此外，受信任的启动器已配置为避免消耗过多的资源。

我们建议使用资源调控器管理附属进程，并根据单个数据库配置和工作负荷的需求优化这些进程。  例如，在执行过程中，可以根据需要创建或销毁任一附属进程。

## <a name="disable-or-enable-external-script-execution"></a>禁用或启用外部脚本执行

支持外部脚本中是可选[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装过程中，并且即使安装完整的外部脚本执行后设置为 OFF 默认情况下，出于安全原因。 因此，已完成之一的机器学习语言和相关的服务的安装后，必须显式重新配置该实例，然后重新启动数据库引擎服务。

发生失控脚本，你可以禁用所有脚本执行。 只需逆向执行此过程，并将该属性设置`external scripts enabled`为 FALSE 或 0，在实例上的。 这将立即禁用任何外部脚本执行。 你应保留安全问题或管理员需要立即缓解资源问题的情况下此选项。

## <a name="see-also"></a>另请参阅

[资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

