---
title: 如何为 SQL Server 机器学习创建资源池 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 12b21a37e66351cb84b6de246f3b398a1d20bfd3
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100550"
---
# <a name="how-to-create-a-resource-pool-for-machine-learning-in-sql-server"></a>如何在 SQL Server 中创建用于机器学习的资源池
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何创建和使用专门用于管理 R 和 Python 机器学习工作负荷在 SQL Server 中的资源池。 它假定已安装并启用机器学习功能，并且想要重新配置以支持更细致地管理 R 或 Python 等外部进程使用的资源的实例。

过程包括多个步骤：

1.  查看任何现有的资源池的状态。 它是必须了解哪些服务正在使用现有资源。
2.  修改服务器资源池。
3.  创建新的资源池外部进程。
4.  创建分类函数来标识外部脚本请求。
5.  验证新的外部资源池捕获 R 或 Python 中的指定客户端或帐户的作业。

适用范围：[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 和 [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

##  <a name="bkmk_ReviewStatus"></a> 查看现有资源池的状态
  
1.  使用如下所示的语句来检查分配给服务器的默认池的资源。
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **示例结果**

    |pool_id|NAME|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|默认值|0|100|0|100|100|0|0|

2.  检查分配到默认**外部**资源池的资源。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **示例结果**

    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|默认值|100|20|0|2|
 
3.  在这些服务器默认设置，外部运行时将很可能资源不足，无法完成大多数任务。 若要改变这种局面，必须按如下所述修改服务器资源用量：
  
    -   减少可由数据库引擎的最大计算机内存。
  
    -   增加外部进程可以使用的最大计算机内存。

## <a name="modify-server-resource-usage"></a>修改服务器资源用量

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中运行以下语句，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存用量限制为“最大服务器内存”设置中的值的 **60%**。

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  同样，请运行以下语句，将外部进程的内存用量限制为计算机资源总量的 **40%**。
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  若要实施这些更改，必须按如下所示重新配置并重新启动资源调控器：
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  这些是只是建议的设置开始;应该评估您的机器学习任务根据其他服务器进程，以确定如何适当平衡环境和工作负荷。

## <a name="create-a-user-defined-external-resource-pool"></a>创建用户定义的外部资源池
  
1.  对资源调控器配置所做的任何更改将在整个服务器上实施，会影响使用服务器默认池的工作负荷，以及使用外部池的工作负荷。
  
     因此，若要更细致地控制哪些工作负荷优先获得资源，可以新建用户定义的外部资源池。 此外，应定义一个分类函数并将其分配给外部资源池。 **外部**关键字新增功能。
  
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
  
## <a name="create-a-classification-function-for-machine-learning"></a>创建机器学习的分类函数
  
分类函数检查传入的任务，并确定任务是否可以使用当前资源池来运行。 不符合分类函数条件的任务将分配回到服务器的默认资源池。
  
1. 首先，它指定分类器函数应使用资源调控器来确定资源池。 可以将分配**null**的占位符来分类器函数。
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     有关详细信息，请参阅 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)。
  
2.  在每个资源池的分类器函数中，定义的语句或应分配给资源池的传入请求的类型。
  
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

若要验证已进行了更改，应检查为每个与这些实例资源池相关联的工作负荷组的服务器内存和 CPU 配置：

+ 默认池[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务器
+ 外部进程默认资源池
+ 外部进程用户定义的池

1. 运行以下语句以查看所有工作负荷组：

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **示例结果**

    |group_id|NAME|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|内部|Medium|25|0|0|0|0|1|2|
    |2|默认值|Medium|25|0|0|0|0|2|2|
    |256|ds_wg|Medium|25|0|0|0|0|2|256|
  
2.  使用新的目录视图[sys.resource_governor_external_resource_pools &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)，以查看所有外部资源池。
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **示例结果**
    
    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|默认值|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     有关详细信息，请参阅[资源调控器目录视图 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。
  
3.  运行以下语句以返回到外部资源池关联的计算机资源有关的信息，如果适用：
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     在本例中，由于池是使用 AUTO 相关性创建的，因此未显示任何信息。 有关详细信息，请参阅 [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。

## <a name="see-also"></a>请参阅

有关管理服务器资源的详细信息，请参阅：

+  [资源调控器](../../relational-databases/resource-governor/resource-governor.md) 
+ [与资源调控器相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

有关机器学习的资源调控的概述，请参阅：

+  [机器学习服务的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)
