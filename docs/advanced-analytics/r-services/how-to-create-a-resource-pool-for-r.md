---
title: "如何为 R 创建资源池 | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8bf3fa44e0066bd902188c00b1ea72969ff864c0
ms.lasthandoff: 04/11/2017

---
# <a name="how-to-create-a-resource-pool-for-r"></a>如何为 R 创建资源池
  本主题介绍如何创建专门用于管理 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的 R 工作负荷的资源池。 本主题假设你已安装 R Services（数据库内），并想要重新配置 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例来支持更细致地管理 R 使用的资源。  
  
 有关管理服务器资源的详细信息，请参阅[资源调控器](../../relational-databases/resource-governor/resource-governor.md)和[与资源调控器相关的动态管理视图 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。  
  
 **步骤**  
  
1.  查看现有资源池的状态  
  
2.  修改服务器资源池  
  
3.  为外部进程创建新资源池  
  
4.  创建分类函数来标识 R 请求  
  
5.  验证新外部资源池是否捕获 R 作业  
  
##  <a name="bkmk_ReviewStatus"></a> 查看现有资源池的状态  
  
1.  首先，检查分配到服务器默认池的资源。  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **结果**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|默认值|0|100|0|100|100|0|0|  

2.  检查分配到默认**外部**资源池的资源。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **结果**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|默认值|100|20|0|2|  
 
3.  使用这些服务器默认设置时，R 运行时可能无法获得足够的资源来完成大多数任务。 若要改变这种局面，必须按如下所述修改服务器资源用量：  
  
    -   减少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用的最大计算机内存  
  
    -   增加外部进程可以使用的最大计算机内存  
  
## <a name="modify-server-resource-usage"></a>修改服务器资源用量  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中运行以下语句，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存用量限制为“最大服务器内存”设置中的值的 **60%**。  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  同样，请运行以下语句，将外部进程的内存用量限制为计算机资源总量的 **40%**。  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  若要实施这些更改，必须按如下所示重新配置并重新启动资源调控器：  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  这些设置只是建议你最初使用的设置；应该根据其他服务器进程评估 R 要求，确定如何适当平衡环境和工作负荷的设置。  
  
## <a name="create-a-user-defined-external-resource-pool"></a>创建用户定义的外部资源池  
  
1.  对资源调控器配置所做的任何更改将在整个服务器上实施，会影响使用服务器默认池的工作负荷，以及使用外部池的工作负荷。  
  
     因此，若要更细致地控制哪些工作负荷优先获得资源，可以新建用户定义的外部资源池。 此外，应定义一个分类函数并将其分配给外部资源池。  
  
     首先，新建*用户定义的外部资源池*。 在以下示例中，池命名为 **ds_ep**。  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     请注意新的 **EXTERNAL** 关键字。  
  
2.  创建名为 `ds_wg` 的工作负荷组用于管理会话请求。 对于 SQL 查询，将使用默认池；对于所有外部进程查询，将使用 `ds_ep` 池。  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     每当请求无法分类，或者发生其他任何分类失败时，请求将分配到默认组。  
  
     有关详细信息，请参阅[资源调控器工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md)和 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)。  
  
## <a name="create-a-classification-function-for-r"></a>为 R 创建分类函数  
  
1.  分类函数检查传入的任务，并确定任务是否可以使用当前资源池来运行。 不符合分类函数条件的任务将分配回到服务器的默认资源池。  
  
     首先，指定资源调控器应使用分类器函数来确定资源池。 可将 null 指定为分类器函数的占位符。  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     有关详细信息，请参阅 [ALTER RESOURCE GOVERNOR (Transact-SQL)](../../t-sql/statements/alter-resource-governor-transact-sql.md)。  
  
2.  在每个资源池的分类器函数中，定义应分配到资源池的语句或传入请求的类型。  
  
     例如，如果发送请求的应用程序是“Microsoft R Host”或“RStudio”，则以下函数将返回分配到用户定义的外部资源池的架构的名称；否则，将返回默认资源池。  
  
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
  
3.  创建该函数后，请重新配置资源组，将新的分类器函数分配到前面定义的外部资源组。  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## <a name="verify-new-resource-pools-and-affinity"></a>验证新资源池和相关性  
  
1.  若要验证是否已做出更改，请检查与所有实例资源池关联的每个工作负荷组的服务器内存和 CPU 配置：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器的默认池、外部进程的默认资源池，以及外部进程的用户定义池。  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **结果**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|内部|Medium|25|0|0|0|0|1|2|  
    |2|默认值|Medium|25|0|0|0|0|2|2|  
    |256|ds_wg|Medium|25|0|0|0|0|2|256|  
  
2.  可以使用新的目录视图 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 查看所有外部资源池。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **结果**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|默认值|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     有关详细信息，请参阅[资源调控器目录视图 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)。  
  
3.  以下语句返回有关已关联到外部资源池的计算机资源的信息。  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     在本例中，由于池是使用 AUTO 相关性创建的，因此未显示任何信息。 有关详细信息，请参阅 [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)。  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [R Services 的资源调控](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  

