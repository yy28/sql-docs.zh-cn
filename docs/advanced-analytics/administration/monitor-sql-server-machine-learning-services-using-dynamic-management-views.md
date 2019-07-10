---
title: 监视使用动态管理视图 (Dmv)-SQL Server 机器学习的 R 和 Python 脚本执行
description: 使用动态管理视图 (Dmv) 监视 SQL Server 机器学习服务中的 R 和 Python 外部脚本执行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 8d701d9e8595eee3a583e913baabc2148af214fe
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681626"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>使用动态管理视图 (Dmv) 监视 SQL Server 机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用动态管理视图 (Dmv) 监视其执行外部脚本 （R 和 Python），资源使用，诊断问题，并优化 SQL Server 机器学习服务中的性能。

在本文中，您会发现特定于 SQL Server 机器学习服务的 Dmv。 您还可以找到显示的示例查询：

+ 设置和机器学习的配置选项
+ 运行外部 R 或 Python 脚本的活动会话
+ R 和 Python 的外部运行时的执行统计信息
+ 有关外部脚本的性能计数器
+ 有关操作系统、 SQL Server 和外部资源池的内存使用量
+ SQL Server 和外部资源池的内存配置
+ 资源调控器资源池，包括外部资源池
+ 对 R 和 Python 已安装的包

有关 Dmv 的详细信息，请参阅[系统动态管理视图](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。

> [!TIP]
> 你还可以使用自定义报表来监视 SQL Server 机器学习服务。 有关详细信息，请参阅[监视机器学习在 Management Studio 中使用自定义报表](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="dynamic-management-views"></a>动态管理视图

监视 SQL Server 中的机器学习工作负荷时，可以使用以下动态管理视图。 若要查询 Dmv，您需要`VIEW SERVER STATE`具有实例的权限。

| 动态管理视图 | type | Description |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | 执行 | 为运行外部脚本的每个活动工作线程帐户都返回一行。 |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | 执行 | 为每种类型的外部脚本请求返回一行。 |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | 执行 | 为服务器维护的每个性能计数器返回一行。 如果使用的搜索条件`WHERE object_name LIKE '%External Scripts%'`，可以使用此信息以查看运行多少个脚本，该脚本在运行使用的身份验证模式或多少 R 或 Python 调用发出针对整个实例。 |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | Resource Governor | 返回有关当前的外部资源池状态信息在资源调控器中，资源池和资源池统计信息的当前配置。 |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | Resource Governor | 返回有关当前的外部资源池配置 CPU 关联信息在资源调控器。 对于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]（每个计划程序都映射到其中的单个处理器）中的每个计划程序，相应地返回一行。 使用此视图可以监视计划程序的情况或标识失控任务。 |

有关监视信息[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]实例，请参阅[目录视图](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)并[资源调控器相关的动态管理视图](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。

## <a name="settings-and-configuration"></a>设置和配置

查看机器学习服务安装设置和配置选项。

![从设置和配置查询输出](media/dmv-settings-and-configuration.png "从设置和配置查询输出")

运行查询以获得此输出。 有关的视图和函数使用的详细信息，请参阅[sys.dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)， [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)，并[SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)。

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

该查询将返回以下列：

| “列” | Description |
|--------|-------------|
| IsMLServicesInstalled | 如果 SQL Server 机器学习服务安装的实例，则返回 1。 否则，返回 0。 |
| ExternalScriptsEnabled | 如果为实例启用外部脚本，则返回 1。 否则，返回 0。 |
| ImpliedAuthenticationEnabled | 启用返回 1; 如果隐含身份验证。 否则，返回 0。 通过验证登录名是否存在 SQLRUserGroup 检查隐式身份验证的配置。 |
| IsTcpEnabled | 如果为实例启用 TCP/IP 协议，则返回 1。 否则，返回 0。 有关详细信息，请参阅[默认 SQL Server 网络协议配置](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)。 |

## <a name="active-sessions"></a>Active sessions

查看运行外部脚本的活动会话。

![活动设置查询的输出](media/dmv-active-sessions.png "活动设置查询的输出")

运行查询以获得此输出。 使用的动态管理视图的详细信息，请参阅[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)， [sys.dm_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)，并[sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)。

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

该查询将返回以下列：

| “列” | Description |
|--------|-------------|
| session_id | 标识与每个活动主连接关联的会话。 |
| blocking_session_id | 正在阻塞请求的会话的 ID。 如果此列为 NULL，则表示请求未被阻塞，或锁定会话的会话信息不可用（或无法进行标识）。 |
| status | 请求的状态。 |
| database_name | 每个会话的当前数据库的名称。 |
| login_name | 会话当前在其下执行的 SQL Server 登录名。 |
| wait_time | 如果请求当前被阻塞，则此列返回当前等待的持续时间（以毫秒为单位）。 不可为 null。 |
| wait_type | 如果请求当前被阻塞，则此列返回等待类型。 等待类型的信息，请参阅[sys.dm_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 |
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

查看适用于 R 和 Python 外部运行时的执行统计信息。 当前提供的 RevoScaleR、 revoscalepy 或 microsoftml 包函数仅统计信息。

![执行统计信息查询的输出](media/dmv-execution-statistics.png "的执行统计信息查询输出")

运行查询以获得此输出。 使用的动态管理视图的详细信息，请参阅[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 该查询仅返回已超过一次执行的函数。

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

该查询将返回以下列：

| “列” | Description |
|--------|-------------|
| language | 已注册的外部脚本语言的名称。 |
| counter_name | 已注册的外部脚本函数的名称。 |
| counter_value | 已在服务器上调用已注册外部脚本函数的实例的总数。 此值是累计的（从在实例上安装该功能的时间开始），且不能重置。 |

## <a name="performance-counters"></a>性能计数器

查看与外部脚本的执行相关的性能计数器。

![输出从性能计数器查询](media/dmv-performance-counters.png "输出从性能计数器查询")

运行查询以获得此输出。 使用的动态管理视图的详细信息，请参阅[sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)。

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**sys.dm_os_performance_counters**输出外部脚本的以下性能计数器：

| 计数器 | Description |
|---------|-------------|
| 执行总次数 | 通过本地或远程调用启动的外部进程数。 |
| 并行执行 | 脚本包含的次数 _@parallel_ 规范和的[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]能够生成并使用并行查询计划。 |
| 流式执行 | 流式处理功能调用次数。 |
| SQL CC 执行 | 作为计算上下文使用的运行位置调用远程实例化和 SQL Server 的外部脚本的数量。 |
| 默示身份验证。登录名 | 使用隐式身份验证; 进行 ODBC 环回调用的次数也就是说，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]执行代表发送脚本请求的用户调用。 |
| 总执行时间 (ms) | 调用和完成调用之间经过的时间。 |
| 执行错误 | 脚本报告的错误次数。 此计数不包括 R 或 Python 的错误。 |

## <a name="memory-usage"></a>内存使用量

查看有关操作系统、 SQL Server 和外部池使用的内存的信息。

![内存使用情况查询的输出](media/dmv-memory-usage.png "输出从内存使用情况查询")

运行查询以获得此输出。 使用的动态管理视图的详细信息，请参阅[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)并[sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)。

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

该查询将返回以下列：

| “列” | Description |
|--------|-------------|
| physical_memory_kb | 在计算机上的物理内存总量。 |
| committed_kb | 内存管理器中的千字节 (KB) 中的已提交的内存。 不包括内存管理器中的保留内存。 |
| external_pool_peak_memory_kb | 最大内存量之和使用，以千字节，所有外部资源池。 |

## <a name="memory-configuration"></a>内存配置

查看以百分比表示的 SQL Server 和外部资源池的最大内存配置有关的信息。 如果默认值为运行 SQL Server `max server memory (MB)`，它被视为 100%的 OS 的内存。

![内存配置查询的输出](media/dmv-memory-configuration.png "输出从内存配置查询")

运行查询以获得此输出。 使用的视图的详细信息，请参阅[sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)并[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

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

该查询将返回以下列：

| “列” | Description |
|--------|-------------|
| name | SQL Server 的外部资源池的名称。 |
| max_memory_percent | 可使用 SQL Server 或外部资源池的最大内存。 |

## <a name="resource-pools"></a>资源池

中[SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md)即[资源池](../../relational-databases/resource-governor/resource-governor-resource-pool.md)实例的物理资源的子集。 您可以指定限制的 CPU、 物理 IO 和传入应用程序请求，包括执行外部脚本，可以使用资源池内的内存量。 查看 SQL Server 和外部脚本使用的资源池。

![输出从资源池查询](media/dmv-resource-pools.png "输出从资源池查询")

运行查询以获得此输出。 使用的动态管理视图的详细信息，请参阅[sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)并[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

该查询将返回以下列：

| “列” | Description |
|--------|-------------|
| pool_name | 资源池的名称。 SQL Server 资源池都带有前缀`SQL Server`和外部资源池都带有前缀`External Pool`。
| total_cpu_usage_hours | 以毫秒为单位自重置资源调控器统计信息以来累积的 CPU 使用率。 |
| read_io_completed_total | 自重置资源调控器统计信息以来完成的读取 IO 总数。 |
| write_io_completed_total | 自重置资源调控器统计信息以来完成的写入 IO 总数。 |

## <a name="installed-packages"></a>已安装的包

你可以查看安装在 SQL Server 机器学习服务通过执行这些输出的 R 或 Python 脚本的 R 和 Python 包。

### <a name="installed-packages-for-r"></a>安装适用于 R 的包

查看 SQL Server 机器学习服务中安装的 R 包。

![从 R 查询已安装的包输出](media/dmv-installed-packages-r.png "输出从 R 查询已安装的包")

运行查询以获得此输出。 该查询使用 R 脚本来确定 R 包与 SQL Server 安装。

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

返回的列是：

| “列” | Description |
|--------|-------------|
| package | 已安装包的名称。 |
| 版本 | 包的版本。 |
| 依赖的对象 | 列出已安装的包依赖的包。 |
| 许可证 | 已安装的程序包的许可证。 |
| LibPath | 在哪里可以找到包的目录。 |

### <a name="installed-packages-for-python"></a>安装用于 Python 的包

查看安装在 SQL Server 机器学习服务中的 Python 包。

![从 Python 查询已安装的包输出](media/dmv-installed-packages-python.png "输出从 Python 查询已安装的包")

运行查询以获得此输出。 查询使用 Python 脚本来确定 SQL Server 一起安装的 Python 包。

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

返回的列是：

| “列” | Description |
|--------|-------------|
| package | 已安装包的名称。 |
| 版本 | 包的版本。 |
| Location | 在哪里可以找到包的目录。 |

## <a name="next-steps"></a>后续步骤

+ [管理和监视机器学习解决方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [用于机器学习的扩展的事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [与资源调控器相关的动态管理视图](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [系统动态管理视图](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [在 Management Studio 中使用自定义报表监视机器学习](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)