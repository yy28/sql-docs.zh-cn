---
title: R 和 Python 脚本执行的 SQL Server 机器学习的资源调控
description: 为 SQL Server 数据库引擎实例上的 R 和 Python 工作负荷分配 RAM 内存、 CPU 和 IO。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e6063f8367e5b91e7e935d6f92515a6dd452dc56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963136"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL Server 中机器学习的资源调控
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

数据科学和机器学习算法是计算密集型操作。 具体取决于工作负荷的优先级，可能需要增加可用于数据科学的资源或资源如果 R 和 Python 脚本执行减少影响并发运行的其他服务的性能。 

当你需要进行多个工作负载间重新平衡分布的系统资源时，可以使用[资源调控器](../../relational-databases/resource-governor/resource-governor.md)分配 CPU、 物理 IO 和内存资源供外部运行时对 R 和 Python。 如果迁移的资源分配，请记住，您可能需要以便同时减少其他工作负荷和服务保留的内存量。 

> [!NOTE] 
> 资源调控器是企业版功能。

## <a name="default-allocations"></a>默认的分配

默认情况下，机器学习的外部脚本运行时仅限于不超过 20%的总计算机内存。 这取决于您的系统，但一般情况下，你可能会发现此限制不足以严重的机器学习任务，例如为模型定型或预测在很多行数据。 

## <a name="use-resource-governor-to-control-resourcing"></a>使用资源调控器来控制资源
 
默认情况下，外部进程在本地服务器上使用最多 20%的主机内存总量。 可以修改要更改服务器范围内，使用 R 的默认资源池，并利用任何容量的 Python 进程，将提供给外部进程。

或者，可以构造自定义*外部资源池*，与关联的工作负荷组和分类器，来确定从特定程序、 主机或其他条件发起的请求的资源分配的提供。 外部资源池是一种中引入的资源池[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]以帮助管理到数据库引擎外部的 R 和 Python 进程。

1. [启用资源调控](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor)（它默认处于关闭状态）。

2. 运行[CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql)创建和配置资源池后, 跟[ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql)来实现它。

3. 创建进行精细的分配，例如之间定型和计分工作负荷组。

4. 创建分类器来拦截供外部处理的调用。

5. 执行查询和使用你创建的对象的过程。

有关演练，请参阅[如何创建用于外部 R 和 Python 脚本的资源池](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)有关分步说明。

术语和一般概念的介绍，请参阅[资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。

## <a name="processes-under-resource-governance"></a>在资源调控下的进程
  
 可以使用*外部资源池*来管理使用数据库引擎实例上的以下可执行文件的资源：

+ Rterm.exe 时调用从 SQL Server 的本地或远程调用 SQL Server 作为远程计算上下文
+ Python.exe 时调用从 SQL Server 的本地或远程调用 SQL Server 作为远程计算上下文
+ BxlServer.exe 和附属进程
+ 启动快速启动板，如 PythonLauncher.dll 的附属进程
  
> [!NOTE]
> 不支持通过使用资源调控器快速启动板服务的直接管理。 快速启动板是一种受信任的服务，可以仅由 Microsoft 提供的宿主启动器。 受信任的启动器显式配置为避免消耗过多的资源。
  
## <a name="see-also"></a>请参阅

+ [管理机器学习集成](../r/managing-and-monitoring-r-solutions.md)
+ [为机器学习创建资源池](../r/how-to-create-a-resource-pool-for-r.md)
+ [资源调控器资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
