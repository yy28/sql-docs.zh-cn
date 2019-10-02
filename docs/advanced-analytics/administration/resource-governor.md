---
title: 利用 Resource Governor 管理 Python 和 R 工作负荷
description: 了解如何使用 Resource Governor 管理 SQL Server 机器学习服务中的 Python 和 R 工作负荷的 CPU、物理 IO 和内存资源分配。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: eec3d2762366252fbc170c2a6c4176fe0283edce
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714311"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>利用 SQL Server 中的 Resource Governor 管理 Python 和 R 工作负荷机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

了解如何使用[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)管理 SQL Server 机器学习服务中的 Python 和 R 工作负荷的 CPU、物理 IO 和内存资源分配。

Python 和 R 中的机器学习算法通常会占用大量计算资源。 根据你的工作负荷优先级，你可能需要增加或减少可用于机器学习服务的资源。

有关更多常规信息，请参阅[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)。

> [!NOTE] 
> Resource Governor 是企业版功能。

## <a name="default-allocations"></a>默认分配

默认情况下，机器学习的外部脚本运行时限制为不超过总计算机内存的 20%。 这取决于您的系统, 但在一般情况下, 您可能会发现, 对于严重的机器学习任务 (如定型模型或预测多行数据), 此限制不够。 

## <a name="use-resource-governor-to-control-resourcing"></a>使用 Resource Governor 来控制管理
 
默认情况下，外部进程最多可使用本地服务器上的总主机内存的 20%。 您可以修改默认资源池, 以使 R 和 Python 进程利用您向外部进程提供的任何容量。

另外, 还可以通过关联的工作负荷组和分类器来构造自定义*外部资源池*, 以确定源自特定程序、主机或其他条件的请求的资源分配。 外部资源池是中[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]引入的一种资源池, 用于帮助管理数据库引擎外部的 R 和 Python 进程。

1. [启用资源调控](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor)(默认情况下处于关闭状态)。

2. 若要创建和配置资源池, 请运行 "[创建外部资源池](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql)", 然后[更改资源调控](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql)器以实现它。

3. 为粒度分配创建工作负荷组, 例如在定型和评分之间。

4. 创建用于截获外部处理调用的分类器。

5. 使用所创建的对象执行查询和过程。

有关演练, 请参阅[如何创建用于外部 R 和 Python 脚本的资源池](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md), 以获取分步说明。

有关术语和一般概念的介绍, 请参阅[Resource Governor 资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)。

## <a name="processes-under-resource-governance"></a>资源调控下的进程
  
 您可以使用*外部资源池*来管理数据库引擎实例上的以下可执行文件使用的资源:

+ Rterm.exe 从 SQL Server 本地调用, 或以远程计算上下文 SQL Server 远程调用
+ 在本地从 SQL Server 调用或以远程计算上下文 SQL Server 远程调用 Python
+ BxlServer.exe 和附属进程
+ 快速启动板启动的附属进程, 如 PythonLauncher
  
> [!NOTE]
> 不支持通过使用 Resource Governor 直接管理快速启动板服务。 快速启动板是一个受信任的服务, 它只能托管 Microsoft 提供的启动器。 受信任的启动器经过显式配置, 以避免消耗过多的资源。
  
## <a name="next-steps"></a>后续步骤

+ [为机器学习创建资源池](create-external-resource-pool.md)
+ [Resource Governor 资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
