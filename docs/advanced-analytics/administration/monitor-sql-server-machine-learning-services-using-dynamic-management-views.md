---
title: 使用 Dmv 监视 Python 和 R 脚本执行
description: 使用动态管理视图（Dmv）监视 SQL Server 机器学习服务中的 Python 和 R 外部脚本执行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8333da0bd3b5b4ad4f0b377edec110e30565c273
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713181"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>使用动态管理视图 (Dmv) 监视 SQL Server 机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用动态管理视图（Dmv）监视外部脚本（Python 和 R）的执行情况、使用的资源、诊断问题，并 SQL Server 机器学习服务中优化性能。

在本文中, 你将找到特定于 SQL Server 机器学习服务的 Dmv。 你还将找到显示以下内容的示例查询:

+ 机器学习的设置和配置选项
+ 运行外部 Python 或脚本的活动会话
+ 用于 Python 和 R 的外部运行时的执行统计信息
+ 外部脚本的性能计数器
+ OS、SQL Server 和外部资源池的内存使用量
+ SQL Server 和外部资源池的内存配置
+ Resource Governor 资源池, 包括外部资源池
+ 安装的 Python 和 R 包

有关 Dmv 的更多常规信息, 请参阅[系统动态管理视图](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。

> [!TIP]
> 你还可以使用自定义报表监视 SQL Server 机器学习服务。 有关详细信息, 请参阅[在 Management Studio 中使用自定义报表监视机器学习](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="dynamic-management-views"></a>动态管理视图

监视 SQL Server 中的机器学习工作负荷时, 可以使用以下动态管理视图。 若要查询 dmv, 需要`VIEW SERVER STATE`对实例的权限。

| 动态管理视图 | 类型 | 描述 |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | 执行 | 为运行外部脚本的每个活动工作线程帐户都返回一行。 |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | 执行 | 为每种类型的外部脚本请求返回一行。 |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | 执行 | 为服务器维护的每个性能计数器返回一行。 如果使用搜索条件`WHERE object_name LIKE '%External Scripts%'`, 则可以使用此信息来查看运行了多少个脚本, 使用哪种身份验证模式运行了哪些脚本, 或者对实例上发出了多少个 R 或 Python 调用。 |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | Resource Governor | 返回 Resource Governor 中当前外部资源池状态、资源池的当前配置以及资源池统计信息的信息。 |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | Resource Governor | 返回 Resource Governor 中当前外部资源池配置的 CPU 关联信息。 对于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]（每个计划程序都映射到其中的单个处理器）中的每个计划程序，相应地返回一行。 使用此视图可以监视计划程序的情况或标识失控任务。 |

有关监视[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]实例的信息, 请参阅[目录视图](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)和[Resource Governor 相关的动态管理视图](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。

## <a name="settings-and-configuration"></a>设置和配置

查看机器学习服务安装设置和配置选项。

![设置和配置查询的输出](media/dmv-settings-and-configuration.png "设置和配置查询的输出")

运行以下查询以获取此输出。 有关所使用的视图和函数的详细信息, 请参阅[_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md), [configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)和[SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)。

```sql
SELECT CAST(SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS INT) AS IsMLServicesInstalled
    , CAST(value_in_use AS INT) AS ExternalScriptsEnabled
    , COALESCE(SIGN(SUSER_ID(CONCAT (
                    CAST(SERVERPROPERTY('MachineName') AS NVARCHAR(128))
                    , '\SQLRUserGroup'
                    , CAST(serverproperty('InstanceName') AS NVARCHAR(128))
                    ))), 0) AS ImpliedAuthenticationEnabled
    , COALESCE((
            SELECT CAST(r.value_data AS INT)
            FROM sys.dm_server_registry AS r
            WHERE r.registry_key LIKE 'HKLM\Software\Microsoft\Microsoft SQL Server\%\SuperSocketNetLib\Tcp'
            AND r.value_name = 'Enabled'
            ), - 1) AS IsTcpEnabled
FROM sys.configurations
WHERE name = 'external scripts enabled';
```

查询返回以下列:

| “列” | 描述 |
|--------|-------------|
| IsMLServicesInstalled | 如果为实例安装 SQL Server 机器学习服务, 则返回1。 否则, 返回0。 |
| ExternalScriptsEnabled | 如果为实例启用了外部脚本, 则返回1。 否则, 返回0。 |
| ImpliedAuthenticationEnabled | 如果启用隐含身份验证, 则返回1。 否则, 返回0。 通过验证是否存在 SQLRUserGroup 的登录名来检查隐含身份验证的配置。 |
| IsTcpEnabled | 如果为实例启用了 TCP/IP 协议, 则返回1。 否则, 返回0。 有关详细信息, 请参阅[默认 SQL Server 网络协议配置](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)。 |

## <a name="active-sessions"></a>Active sessions

查看正在运行外部脚本的活动会话。

![活动设置查询的输出](media/dmv-active-sessions.png "活动设置查询的输出")

运行以下查询以获取此输出。 有关使用的动态管理视图的详细信息，请参阅[_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)、 [_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)和[sys.databases _exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)。

```sql
SELECT r.session_id, r.blocking_session_id, r.status, DB_NAME(s.database_id) AS database_name
    , s.login_name, r.wait_time, r.wait_type, r.last_wait_type, r.total_elapsed_time, r.cpu_time
    , r.reads, r.logical_reads, r.writes, er.language, er.degree_of_parallelism, er.external_user_name
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_external_script_requests AS er
ON r.external_script_request_id = er.external_script_request_id
INNER JOIN sys.dm_exec_sessions AS s
ON s.session_id = r.session_id;
```

查询返回以下列:

| “列” | 描述 |
|--------|-------------|
| session_id | 标识与每个活动主连接关联的会话。 |
| blocking_session_id | 正在阻塞请求的会话的 ID。 如果此列为 NULL，则表示请求未被阻塞，或锁定会话的会话信息不可用（或无法进行标识）。 |
| status | 请求的状态。 |
| database_name | 每个会话的当前数据库的名称。 |
| login_name | 当前正在执行会话的 SQL Server 登录名。 |
| wait_time | 如果请求当前被阻塞，则此列返回当前等待的持续时间（以毫秒为单位）。 不可为 null。 |
| wait_type | 如果请求当前被阻塞，则此列返回等待类型。 有关等待类型的信息，请参阅[_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 |
| last_wait_type | 如果此请求先前已经阻塞，则此列返回上次等待的类型。 |
| total_elapsed_time | 请求到达后经过的总时间（毫秒）。 |
| cpu_time | 请求所使用的 CPU 时间（毫秒）。 |
| reads | 此请求执行的读取数。 |
| logical_reads | 此请求已经执行的逻辑读取数。 |
| Writes | 此请求执行的写入数。 |
| language | 表示支持的脚本语言的关键字。 |
| degree_of_parallelism | 数字，指示已创建的并行进程数。 此值可能与请求的并行进程数不同。 |
| external_user_name | 在其下执行脚本的 Windows 工作线程帐户。 |

## <a name="execution-statistics"></a>执行统计信息

查看适用于 R 和 Python 的外部运行时的执行统计信息。 只有 RevoScaleR、revoscalepy 或 microsoftml 包函数的统计信息当前可用。

![执行统计信息查询的输出](media/dmv-execution-statistics.png "执行统计信息查询的输出")

运行以下查询以获取此输出。 有关使用的动态管理视图的详细信息，请参阅[_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 查询只返回多次执行的函数。

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

查询返回以下列:

| “列” | 描述 |
|--------|-------------|
| language | 已注册的外部脚本语言的名称。 |
| counter_name | 已注册的外部脚本函数的名称。 |
| counter_value | 已在服务器上调用已注册外部脚本函数的实例的总数。 此值是累计的（从在实例上安装该功能的时间开始），且不能重置。 |

## <a name="performance-counters"></a>性能计数器

查看与执行外部脚本相关的性能计数器。

![性能计数器查询的输出](media/dmv-performance-counters.png "性能计数器查询的输出")

运行以下查询以获取此输出。 有关使用的动态管理视图的详细信息，请参阅[_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)。

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**sys.databases _os_performance_counters**为外部脚本输出以下性能计数器：

| 计数器 | 描述 |
|---------|-------------|
| 执行总次数 | 由本地或远程调用启动的外部进程的数目。 |
| 并行执行 | 脚本包含 _\@并行_规范并且[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]能够生成和使用并行查询计划的次数。 |
| 流式执行 | 已调用流式处理功能的次数。 |
| SQL CC 执行 | 外部脚本运行的次数, 其中远程实例化调用并将 SQL Server 用作计算上下文。 |
| 默示身份验证。登录名 | 使用隐含身份验证进行 ODBC 环回调用的次数;也就是说, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]代表发送脚本请求的用户执行调用。 |
| 总执行时间 (ms) | 调用和完成调用之间经过的时间。 |
| 执行错误 | 脚本报告错误的次数。 此计数不包括 R 或 Python 错误。 |

## <a name="memory-usage"></a>内存使用量

查看有关 OS、SQL Server 和外部池使用的内存的信息。

![内存使用情况查询的输出](media/dmv-memory-usage.png "内存使用情况查询的输出")

运行以下查询以获取此输出。 有关使用的动态管理视图的详细信息，请参阅[sys.databases _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) and [sys.databases _os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)。

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

查询返回以下列:

| “列” | 描述 |
|--------|-------------|
| physical_memory_kb | 计算机上的物理内存总量。 |
| committed_kb | 内存管理器中的提交内存 (KB)。 不包括内存管理器中的保留内存。 |
| external_pool_peak_memory_kb | 所有外部资源池的最大内存量 (以 kb 为单位) 的总和。 |

## <a name="memory-configuration"></a>内存配置

查看 SQL Server 和外部资源池的最大内存配置的相关信息。 如果 SQL Server 运行时的默认值为 `max server memory (MB)`，则将其视为 100% 的 OS 内存。

![内存配置查询的输出](media/dmv-memory-configuration.png "内存配置查询的输出")

运行以下查询以获取此输出。 有关所使用的视图的详细信息，请参阅[sys.databases](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)和[_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```sql
SELECT 'SQL Server' AS name
    , CASE CAST(c.value AS BIGINT)
        WHEN 2147483647 THEN 100
        ELSE (SELECT CAST(c.value AS BIGINT) / (physical_memory_kb / 1024.0) * 100 FROM sys.dm_os_sys_info)
        END AS max_memory_percent
FROM sys.configurations AS c
WHERE c.name LIKE 'max server memory (MB)'
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name, ep.max_memory_percent
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

查询返回以下列:

| “列” | 描述 |
|--------|-------------|
| name | 外部资源池的名称或 SQL Server。 |
| max_memory_percent | SQL Server 或外部资源池可以使用的最大内存。 |

## <a name="resource-pools"></a>资源池

在[SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md)中,[资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)表示实例的物理资源的子集。 可以指定传入应用程序请求的 CPU、物理 IO 和内存量的限制, 包括执行外部脚本, 并且可以在资源池中使用。 查看用于 SQL Server 和外部脚本的资源池。

![资源池查询的输出](media/dmv-resource-pools.png "资源池查询的输出")

运行以下查询以获取此输出。 有关使用的动态管理视图的详细信息，请参阅[sys.databases _resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) and [sys.databases _resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

查询返回以下列:

| “列” | 描述 |
|--------|-------------|
| pool_name | 资源池的名称。 SQL Server 的资源池具有`SQL Server`前缀, 外部资源池以`External Pool`为前缀。
| total_cpu_usage_hours | 重置资源调控器统计信息以来的累计 CPU 使用率 (以毫秒为单位)。 |
| read_io_completed_total | 自重置资源调控器统计信息以来完成的读取 IO 总数。 |
| write_io_completed_total | 自重置资源调控器统计信息以来完成的写入 IO 总数。 |

## <a name="installed-packages"></a>已安装包

可以通过执行输出的 R 或 Python 脚本来查看安装在 SQL Server 机器学习服务中的 R 和 Python 包。

### <a name="installed-packages-for-r"></a>适用于 R 的已安装包

查看安装在 SQL Server 机器学习服务中的 R 包。

![用于 R 查询的已安装包的输出](media/dmv-installed-packages-r.png "用于 R 查询的已安装包的输出")

运行以下查询以获取此输出。 查询使用 R 脚本来确定随 SQL Server 一起安装的 R 包。

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

返回的列包括:

| “列” | 描述 |
|--------|-------------|
| package | 已安装包的名称。 |
| Version | 包的版本。 |
| 依赖的对象 | 列出已安装的包所依赖的包。 |
| 许可证 | 已安装包的许可证。 |
| LibPath | 可在其中找到包的目录。 |

### <a name="installed-packages-for-python"></a>为 Python 安装包

查看 SQL Server 机器学习服务中安装的 Python 包。

![用于 Python 查询的已安装包的输出](media/dmv-installed-packages-python.png "用于 Python 查询的已安装包的输出")

运行以下查询以获取此输出。 查询使用 Python 脚本来确定随 SQL Server 一起安装的 Python 包。

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

返回的列包括:

| “列” | 描述 |
|--------|-------------|
| package | 已安装包的名称。 |
| Version | 包的版本。 |
| Location | 可在其中找到包的目录。 |

## <a name="next-steps"></a>后续步骤

+ [管理和监视机器学习解决方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [机器学习的扩展事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Resource Governor 相关的动态管理视图](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [系统动态管理视图](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [在 Management Studio 中使用自定义报表监视机器学习](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
