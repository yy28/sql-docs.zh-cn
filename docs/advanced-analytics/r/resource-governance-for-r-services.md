---
title: "SQL Server 中的机器学习的资源调控 |Microsoft 文档"
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d1eb0f1cce23d084516b5446d39274ac3078b0b8
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL Server 中的机器学习的资源调控
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供的资源调控概述 SQL Server 中的功能来帮助分配和平衡使用 R 和 Python 脚本的资源。

**适用于：** [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)]
 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]和 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]

## <a name="goals-of-resource-governance-for-machine-learning"></a>机器学习的资源调控的目标

一个与 R 和 Python 等的机器学习语言的已知的难点是数据到不受计算机通常移动于数据库外部的 IT。 另一个是，R 是单线程，这意味着你可以仅使用中内存可用的数据。 

SQL Server 计算机学习 Services 来缓解这两个问题，并帮助满足企业法规遵从性要求。 保存在数据库内的高级的分析和支持通过通过流式处理和分块操作等功能的大型数据集的更高的性能。 但是，移动数据库内的 R 和 Python 计算，这种情况可能会影响使用数据库，包括常规用户查询、 外部应用程序和计划的数据库作业的其他服务的性能。

本部分提供有关如何管理外部运行时，如 R 和 Python，用于减少对其他核心数据库服务的影响资源的信息。 数据库服务器环境通常是多个从属应用程序和服务的集线器。

你可以使用[资源调控器](../../relational-databases/resource-governor/resource-governor.md)来管理 R 和 Python 的外部运行时使用的资源。  对于机器学习中，资源调控包括这些任务：

+ 识别使用过多服务器资源的脚本。
  
     管理员需要能够终止或限制消耗过多资源的作业。
  
+ 消减不可预测的工作负荷。
  
     例如，如果在服务器上同时运行多个计算机学习作业，生成的资源争用无法导致不可预测的性能，或可能完成的工作负荷。 但是，如果使用资源池，作业可以相互隔离的。
  
-   排定工作负荷的优先级。
  
     管理员或架构师需要能够指定必须优先，或确保某些工作负荷要在资源争用时完成的工作负荷。

## <a name="how-to-use-resource-governor-to-manage-machine-learning"></a>如何使用资源调控器来管理机器学习
 
管理资源分配给 R 或 Python 的会话中，通过创建*外部资源池*，并将工作负荷分配到池或池。 外部资源池是一种新中引入的资源池[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]以帮助管理 R 运行时和其他处理到数据库引擎外部。

SQL Server 支持三种类型的默认资源池： 
  
-   *内部池*表示 SQL Server 本身使用的、不可更改或限制的资源。
  
-   *默认池*是预定义的用户池，可用于修改整个服务器的资源用量。 还可以定义属于此池的用户组，以管理对资源的访问。
  
-   *默认外部池*是外部资源的预定义用户池。 此外，可以创建新的外部资源池，并定义属于此池的用户组。
  
 还可以创建*用户定义的资源池*将资源分配到数据库引擎或其他应用程序，创建*用户定义的外部资源池*来管理 R 和其他外部进程。
  
 有关术语和一般概念的全面介绍，请参阅[资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。

  
## <a name="resource-management-walkthrough-with-resource-governor"></a>资源管理演练资源调控器

如果你不熟悉到资源调控器，请参阅本主题有关如何修改实例默认资源并创建新的外部资源池的快速演练：[创建外部脚本的资源池](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)
  
 你可以使用*外部资源池*机制来管理使用机器学习中使用的以下可执行文件的资源：

+ Rterm.exe 和附属进程
+ Python.exe 和附属进程
+ BxlServer.exe 和附属进程
+ 附属进程启动快速启动板
  
> [!NOTE]
> 
> 不支持通过使用资源调控器的快速启动板服务的直接管理。 这是因为 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 是一个受信任的服务，在设计上只能托管 Microsoft 提供的启动器。 受信任的启动器配置以避免过度消耗资源。
>   
> 我们建议使用资源调控器管理附属进程，并根据单个数据库配置和工作负荷的需求优化这些进程。  例如，在执行过程中，可以根据需要创建或销毁任一附属进程。
  
## <a name="disable-external-script-execution"></a>禁用外部脚本执行

在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 过程中，对外部脚本的支持是可选的。 在安装机器学习功能后, 能够执行外部脚本默认情况下，为 OFF 和您必须手动重新配置属性，并重新启动要启用脚本执行的实例。

因此，如果需要立即，缓解资源问题或安全问题，管理员可以立即禁用任何外部脚本执行使用[sp_configure & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)和设置属性`external scripts enabled`为 FALSE 或 0。
  
## <a name="see-also"></a>另请参阅

[管理和监视机器学习解决方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)

[为机器学习创建资源池](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

[资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
