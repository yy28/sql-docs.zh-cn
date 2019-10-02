---
title: 为 Python 和 R 创建资源池
description: 了解如何创建和使用资源池来管理 SQL Server 机器学习服务中的 Python 和 R 工作负荷。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8e8c48665c2928a0c8133892cc0029b4bd82c4cc
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714321"
---
# <a name="create-a-resource-pool-for-sql-server-machine-learning-services"></a>为 SQL Server 创建资源池机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

了解如何创建和使用资源池来管理 SQL Server 机器学习服务中的 Python 和 R 工作负荷。 

此过程包括多个步骤:

1. 查看任何现有资源池的状态。 了解使用现有资源的服务非常重要。
2. 修改服务器资源池。
3. 为外部进程创建新的资源池。
4. 创建用于标识外部脚本请求的分类函数。
5. 验证新的外部资源池是否正在从指定的客户端或帐户捕获 R 或 Python 作业。

<a name="bkmk_ReviewStatus"></a>

##  <a name="review-the-status-of-existing-resource-pools"></a>查看现有资源池的状态
  
1.  使用如下所示的语句来检查分配给服务器的默认池的资源。
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **示例结果**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|默认值|0|100|0|100|100|0|0|

2.  检查分配到默认**外部**资源池的资源。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **示例结果**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|默认值|100|20|0|2|
 
3.  在这些服务器默认设置下, 外部运行时可能资源不足, 无法完成大多数任务。 若要改变这种局面，必须按如下所述修改服务器资源用量：
  
    -   减少数据库引擎可使用的最大计算机内存。
  
    -   增加外部进程可使用的最大计算机内存。

## <a name="modify-server-resource-usage"></a>修改服务器资源用量

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中运行以下语句，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存用量限制为“最大服务器内存”设置中的值的 **60%** 。

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  同样，请运行以下语句，将外部进程的内存用量限制为计算机资源总量的 **40%** 。
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  若要实施这些更改，必须按如下所示重新配置并重新启动资源调控器：
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  这些只是建议的设置, 以开始:你应在其他服务器进程中评估你的机器学习任务, 以确定你的环境和工作负荷的正确平衡点。

## <a name="create-a-user-defined-external-resource-pool"></a>创建用户定义的外部资源池
  
1.  对资源调控器配置所做的任何更改将在整个服务器上实施，会影响使用服务器默认池的工作负荷，以及使用外部池的工作负荷。
  
     因此，若要更细致地控制哪些工作负荷优先获得资源，可以新建用户定义的外部资源池。 此外，应定义一个分类函数并将其分配给外部资源池。 **EXTERNAL**关键字是新的。
  
     首先，新建*用户定义的外部资源池*。 在以下示例中，池命名为 **ds_ep**。
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  创建名为 `ds_wg` 的工作负荷组用于管理会话请求。 对于 SQL 查询，将使用默认池；对于所有外部进程查询，将使用 `ds_ep` 池。
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     每当请求无法分类，或者发生其他任何分类失败时，请求将分配到默认组。
  
     有关详细信息，请参阅[资源调控器工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md)和 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)。
  
## <a name="create-a-classification-function-for-machine-learning"></a>为机器学习创建分类函数
  
分类函数检查传入的任务，并确定任务是否可以使用当前资源池来运行。 不符合分类函数条件的任务将分配回到服务器的默认资源池。
  
1. 首先指定 Resource Governor 应使用分类器函数来确定资源池。 可以将**null**指定为分类器函数的占位符。
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     有关详细信息，请参阅 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)。
  
2.  在每个资源池的分类器函数中, 定义应分配给资源池的语句或传入请求的类型。
  
     例如，如果发送请求的应用程序是“Microsoft R Host”或“RStudio”，则以下函数将返回分配到用户定义的外部资源池的架构的名称；否则，将返回默认资源池。
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  创建该函数后，请重新配置资源组，将新的分类器函数分配到前面定义的外部资源组。
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR WITH reconfigure;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>验证新资源池和相关性

若要验证是否进行了更改, 应检查与这些实例资源池关联的每个工作负荷组的服务器内存和 CPU 配置:

+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务器的默认池
+ 外部进程的默认资源池
+ 外部进程的用户定义池

1. 运行以下语句以查看所有工作负荷组:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **示例结果**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|内部|Medium|25|0|0|0|0|1|2|
    |2|默认值|Medium|25|0|0|0|0|2|2|
    |256|ds_wg|Medium|25|0|0|0|0|2|256|
  
2.  使用新的目录视图[resource_governor_external_resource_pools &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)来查看所有外部资源池。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **示例结果**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|默认值|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     有关详细信息，请参阅[资源调控器目录视图 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。
  
3.  运行以下语句, 返回有关关联到外部资源池的计算机资源的信息 (如果适用):
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     在本例中，由于池是使用 AUTO 相关性创建的，因此未显示任何信息。 有关详细信息，请参阅 [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。

## <a name="next-steps"></a>后续步骤

有关管理服务器资源的详细信息, 请参阅:

+ [资源调控器](../../relational-databases/resource-governor/resource-governor.md) 
+ [Resource Governor 相关的动态管理&#40;视图 transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

有关机器学习的资源调控概述, 请参阅:

+ [利用 SQL Server 中的 Resource Governor 管理 Python 和 R 工作负荷机器学习服务](resource-governor.md)
