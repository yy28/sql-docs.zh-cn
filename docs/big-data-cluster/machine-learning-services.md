---
title: 机器学习服务 (Python、R)
titleSuffix: SQL Server Big Data Clusters
description: 了解如何通过机器学习服务在 SQL Server 大数据群集的主实例上运行 Python 和 R 脚本。
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: e16304765e5f4a51feed4d3d59e790505baa740d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252027"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>通过机器学习服务在 SQL Server 大数据群集上运行 Python 和 R 脚本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

可以通过[机器学习服务](../advanced-analytics/index.yml)在 [SQL Server 大数据群集](big-data-cluster-overview.md)的主实例上运行 Python 和 R 脚本。

> [!NOTE]
> 还可以通过 [SQL Server 语言扩展](../language-extensions/language-extensions-overview.md)在主实例上运行 Java 代码。 按照以下步骤操作还将启用语言扩展。

## <a name="enable-machine-learning-services"></a>启用机器学习服务

机器学习服务默认安装在大数据群集上，并且不需要单独安装。

若要启用机器学习服务，请在主实例上运行以下语句：

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

## <a name="enable-always-on-availability-groups"></a>启用 AlwaysOn 可用性组

如果将 SQL Server 大数据群集与 [Always On 可用性组](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)一起使用，则需要执行一些额外的步骤以启用机器学习服务。

1. 连接到主实例并运行以下语句：

    ```sql
    SELECT @@SERVERNAME
    ```

    记下服务器名称。 在此示例中，主实例的服务器名称为 master-2  。

1. 在大数据群集中 Always On 可用性组上的每个副本上，运行以下 `kubectl` 命令：

    ```
    kubectl -n bdc expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer

    kubectl -n bdc expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer

    kubectl -n bdc expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer
    ```

    应该会看到与下面类似的输出：
    
    ```
    service/mymaster-0 exposed

    service/mymaster-1 exposed

    service/mymaster-2 exposed
    ```

1. 连接到每个主副本终结点并启用脚本执行。

    运行以下语句：

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

现在可以在大数据群集的主实例上运行 Python 和 R 脚本。 请参阅下面的快速入门，运行第一个脚本。

## <a name="next-steps"></a>后续步骤

+ [快速入门：通过 SQL Server 机器学习服务创建和运行简单的 Python 脚本](../advanced-analytics/tutorials/quickstart-python-create-script.md)
+ [快速入门：通过 SQL Server 机器学习服务在 Python 中创建预测模型并对其进行评分](../advanced-analytics/tutorials/quickstart-python-train-score-model.md)
+ [快速入门：通过 SQL Server 机器学习服务创建和运行简单的 R 脚本](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [快速入门：通过 SQL Server 机器学习服务在 R 中创建预测模型并对其进行评分](../advanced-analytics/tutorials/quickstart-r-train-score-model.md)
