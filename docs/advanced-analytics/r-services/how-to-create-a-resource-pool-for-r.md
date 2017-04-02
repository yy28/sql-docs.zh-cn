---
title: "如何︰ 为 R 创建资源池 | Microsoft Docs"
ms.custom: ""
ms.date: "10/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# 如何︰ 为 R 创建资源池
  本主题介绍如何创建专用于管理 R 中的工作负荷的资源池 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 它假定您已经安装了 R 服务 （数据库），并且需要重新配置 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例以支持由.的资源的多个严格管理  
  
 有关管理服务器资源的详细信息，请参阅 [资源调控器](../../relational-databases/resource-governor/resource-governor.md) 和 [资源调控器相关动态管理视图和 #40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。  
  
 **步骤**  
  
1.  查看现有资源池的状态  
  
2.  修改服务器资源池  
  
3.  创建新的资源池的外部进程  
  
4.  创建分类函数来标识 R 请求  
  
5.  验证新的外部资源池正在捕获 R 作业  
  
##  <a name="bkmk_ReviewStatus"></a> 查看现有资源池的状态  
  
1.  首先，检查分配给服务器的默认池的资源。  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **结果**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|默认值|0|100|0|100|100|0|0|  

2.  检查分配给默认值的资源 **外部** 资源池。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **结果**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|默认值|100|20|0|2|  
 
3.  在这些服务器默认设置，R 运行时将可能具有资源不足，无法完成大部分任务。 若要更改此设置，必须按以下方式修改服务器资源使用情况︰  
  
    -   减少可由最大计算机内存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   增加可由外部进程的最大计算机内存  
  
## 修改服务器资源使用情况  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ，运行以下语句以限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存使用情况与 **60%** 的最大服务器内存设置中的值。  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  同样，运行以下语句以限制的内存使用外部进程对 **40%** 的总计算机资源。  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  若要强制实施这些更改，必须重新配置并重新启动资源调控器，如下所示︰  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  它们只是建议的设置来启动与;您应该评估 R 的要求和其他服务器进程以确定您的环境和工作负荷的正确余额。  
  
## 创建用户定义的外部资源池  
  
1.  配置资源调控器的任何更改会强制执行整个服务器作为一个整体，并影响对于服务器，请使用默认池的工作负荷，以及使用外部池的工作负荷。  
  
     因此，若要提供更细致的控制哪些工作负荷应该有优先级，可以创建新的用户定义的外部资源池。 此外应定义分类的函数，并将其分配给外部的资源池。  
  
     首先，创建一个新 *用户定义的外部资源池*。 在下面的示例中，名为该池 **ds_ep**。  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     请注意新 **外部** 关键字。  
  
2.  创建一个名为的工作负荷组 `ds_wg` 用于管理会话请求。 对于 SQL 查询中，你将使用默认池;对于所有外部进程的查询将使用 `ds_ep` 池。  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     请求分配给默认组中，只要该请求不能归类，或如果没有任何其他分类失败。  
  
     有关详细信息，请参阅 [资源调控器工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md) 和 [CREATE WORKLOAD GROUP &#40;Transact SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md)。  
  
## 为 R 创建分类函数  
  
1.  分类函数检查传入的任务，并确定该任务是一个可以使用当前的资源池来运行。 返回到服务器的默认资源池分配不满足条件的分类函数任务。  
  
     从指定的分类器函数应由资源调控器以确定资源池的开始。 可以将 null 分配作为分类器函数的占位符。  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     有关详细信息，请参阅 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)。  
  
2.  在每个资源池的分类器函数中，您定义的语句或应分配给资源池的传入请求的类型。  
  
     例如，以下函数将返回分配给用户定义的外部资源池的应用程序发送请求 Microsoft R 主机或 RStudio; 如果该架构的名称否则，返回默认资源池。  
  
    ```  
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
  
3.  当创建该函数后时，重新配置要将新的分类器函数赋给前面定义的外部资源组的资源组。  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## 验证新的资源池和相关性  
  
1.  若要验证是否已做的更改，请检查用于每个工作负荷组与实例的所有资源池相关联的服务器内存和 CPU 配置︰ 默认池适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器、 外部进程的默认资源池和外部进程的用户定义池。  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **结果**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|内部|Medium|25|0|0|0|0|1|2|  
    |2|默认值|Medium|25|0|0|0|0|2|2|  
    |256|ds_wg|Medium|25|0|0|0|0|2|256|  
  
2.  可以使用新的目录视图中， [sys.resource_governor_external_resource_pools &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), ，若要查看所有外部的资源池。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **结果**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|默认值|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     有关详细信息，请参阅 [资源调控器目录视图和 #40;Transact SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。  
  
3.  下面的语句返回到外部资源池将关联的计算机资源有关的信息。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     在这种情况下，使用 AUTO 的关联创建了池，因为不会显示信息。 有关详细信息，请参阅 [sys.dm_resource_governor_resource_pool_affinity &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。  
  
## 另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [R 服务的资源调控](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  