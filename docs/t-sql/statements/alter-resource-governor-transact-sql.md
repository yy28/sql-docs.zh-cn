---
title: "更改资源调控器 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER RESOURCE GOVERNOR
- ALTER_RESOURCE_GOVERNOR_TSQL
- ALTER RESOURCE GOVERNOR RECONFIGURE
- ALTER_RESOURCE_GOVERNOR_RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE GOVERNOR
- RECONFIGURE, ALTER RESOURCE GOVERNOR
ms.assetid: 442c54bf-a0a6-4108-ad20-db910ffa6e3c
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ac7ae791ec7867b13a8547ec60436f25536cd5b7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-resource-governor-transact-sql"></a>ALTER RESOURCE GOVERNOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此语句用于执行中的以下资源调控器操作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   应用配置更改时，指定创建 |ALTER |DROP WORKLOAD GROUP 或创建 |ALTER |DROP RESOURCE POOL 或创建 |ALTER |发出 DROP EXTERNAL RESOURCE POOL 语句。  
  
-   启用或禁用资源调控器。  
  
-   配置传入请求的分类。  
  
-   重置工作负荷组和资源池统计信息。  
  
-   设置每个磁盘卷的最大 I/O 操作数。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER RESOURCE GOVERNOR   
      { DISABLE | RECONFIGURE }  
    | WITH ( CLASSIFIER_FUNCTION = { schema_name.function_name | NULL } )  
    | RESET STATISTICS  
    | WITH ( MAX_OUTSTANDING_IO_PER_VOLUME = value )   
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 DISABLE  
 禁用资源调控器。 禁用资源调控器会产生下列结果：  
  
-   不执行分类器函数。  
  
-   所有新连接被自动分类到默认组中。  
  
-   系统发起的请求被分类到内部工作负荷组中。  
  
-   所有现有的工作负荷组和资源池设置被重置为其默认值。 在这种情况下，到达限制时不触发任何事件。  
  
-   正常的系统监视不受影响。  
  
-   可以进行配置更改，但所做的更改直到启用资源调控器不会生效。  
  
-   在重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，资源调控器不会加载其配置，而是只具有默认的和内部的组和池。  
  
 RECONFIGURE  
 当未启用资源调控器时，RECONFIGURE 可启用资源调控器。 启用资源调控器会产生以下结果：  
  
-   为新连接执行分类器函数，以便可以将其工作负荷分配到工作负荷组。  
  
-   遵守并强制执行资源调控器配置中指定的资源限制。  
  
-   资源调控器已被禁用时所做的任何配置更改会影响启用资源调控器之前已存在的请求。  
  
 当运行资源调控器时，重新配置应用任何配置更改请求时创建 |ALTER |DROP WORKLOAD GROUP 或创建 |ALTER |DROP RESOURCE POOL 或创建 |ALTER |DROP EXTERNAL RESOURCE POOL 语句执行。  
  
> [!IMPORTANT]  
>  必须发出 ALTER RESOURCE GOVERNOR RECONFIGURE 才能使任何配置更改生效。  
  
 CLASSIFIER_FUNCTION = { *schema_name***。***function_name* |NULL}  
 注册指定的分类函数*schema_name.function_name*。 该函数将每个新会话进行分类并将会话请求和查询分配到工作负荷组。 如果使用 NULL，新会话将自动分配到默认工作负荷组。  
  
 RESET STATISTICS  
 重置有关所有工作负荷组和资源池的统计信息。 有关详细信息，请参阅[sys.dm_resource_governor_workload_groups &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)和[sys.dm_resource_governor_resource_pools &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
 MAX_OUTSTANDING_IO_PER_VOLUME =*值*  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 设置每个磁盘卷的最大排队 I/O 操作数。 这些 I/O 操作可以是任何大小的读取或写入。  MAX_OUTSTANDING_IO_PER_VOLUME 的最大值为 100。 它不是百分比。 此设置用于将 IO 资源调控优化为磁盘卷的 IO 特性。 我们建议你的不同值进行试验，并考虑使用等 IOMeter，校准工具[DiskSpd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223)，或 SQLIO （已弃用） 来标识存储子系统的最大值。 此设置进行系统级安全检查，它使 SQL Server 可满足资源池的最小 IOPS，即使其他池将 MAX_IOPS_PER_VOLUME 设置为无限也是如此。 有关 MAX_IOPS_PER_VOLUME 的详细信息，请参阅[CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md)。  
  
## <a name="remarks"></a>注释  
 ALTER RESOURCE GOVERNOR DISABLE、ALTER RESOURCE GOVERNOR RECONFIGURE 和 ALTER RESOURCE GOVERNOR RESET STATISTICS 无法在用户事务内部使用。  
  
 RECONFIGURE 参数是资源调控器语法的一部分，不应与混淆[重新配置](../../t-sql/language-elements/reconfigure-transact-sql.md)，这是一个单独的 DDL 语句。  
  
 建议您先了解资源调控器的状态，然后再执行 DDL 语句。 有关详细信息，请参阅[资源调控器](../../relational-databases/resource-governor/resource-governor.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-starting-the-resource-governor"></a>A. 启动资源调控器  
 初次安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，资源调控器处于禁用状态。 以下示例启动资源调控器。 执行语句后，资源调控器将运行并且可使用预先定义的工作负荷组和资源池。  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="b-assigning-new-sessions-to-the-default-group"></a>B. 将新会话分配到默认组  
 以下示例通过从资源调控器配置删除任何现有分类器函数，将所有新会话分配到默认工作负荷组。 如果没有函数指定为分类器函数，所有新会话将分配到默认工作负荷组。 此更改仅应用于新会话。 现有会话不受影响。  
  
```  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = NULL);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="c-creating-and-registering-a-classifier-function"></a>C. 创建和注册分类器函数  
 以下示例创建一个名为 `dbo.rgclassifier_v1` 的分类器函数。 该函数基于用户名或应用程序名称对每个新会话进行分类，并且将会话请求和查询分配到特定工作负荷组。 未映射到指定用户或应用程序名称的会话将分配到默认工作负荷组。 然后，注册分类器函数并应用配置更改。  
  
```  
-- Store the classifier function in the master database.  
USE master;  
GO  
SET ANSI_NULLS ON;  
GO  
SET QUOTED_IDENTIFIER ON;  
GO  
CREATE FUNCTION dbo.rgclassifier_v1() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
-- Declare the variable to hold the value returned in sysname.  
    DECLARE @grp_name AS sysname  
-- If the user login is 'sa', map the connection to the groupAdmin  
-- workload group.   
    IF (SUSER_NAME() = 'sa')  
        SET @grp_name = 'groupAdmin'  
-- Use application information to map the connection to the groupAdhoc  
-- workload group.  
    ELSE IF (APP_NAME() LIKE '%MANAGEMENT STUDIO%')  
        OR (APP_NAME() LIKE '%QUERY ANALYZER%')  
            SET @grp_name = 'groupAdhoc'  
-- If the application is for reporting, map the connection to  
-- the groupReports workload group.  
    ELSE IF (APP_NAME() LIKE '%REPORT SERVER%')  
        SET @grp_name = 'groupReports'  
-- If the connection does not map to any of the previous groups,  
-- put the connection into the default workload group.  
    ELSE  
        SET @grp_name = 'default'  
    RETURN @grp_name  
END;  
GO  
-- Register the classifier user-defined function and update the   
-- the in-memory configuration.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION=dbo.rgclassifier_v1);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="d-resetting-statistics"></a>D. 重置统计信息  
 以下示例重置所有工作负荷组和资源池统计信息。  
  
```  
ALTER RESOURCE GOVERNOR RESET STATISTICS;  
```  
  
### <a name="e-setting-the-maxoutstandingiopervolume-option"></a>E. 设置 MAX_OUTSTANDING_IO_PER_VOLUME 选项  
 以下示例将 MAX_OUTSTANDING_IO_PER_VOLUME 选项设置为 20。  
  
```  
ALTER RESOURCE GOVERNOR  
WITH (MAX_OUTSTANDING_IO_PER_VOLUME = 20);   
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL (Transact-SQL)](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL (Transact-SQL)](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER 外部资源池 &#40;Transact SQL &#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.dm_resource_governor_workload_groups &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.dm_resource_governor_resource_pools &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)  
  
  

