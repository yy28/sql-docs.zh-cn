---
title: 新增功能
description: 查看 Microsoft 分析平台系统中新增功能，这是托管 MPP SQL Server 并行数据仓库的横向扩展本地设备。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: faf3bd1f487fb5c850759fdde3ddecd32bdd3b1f
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625543"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>分析平台系统（横向扩展 MPP 数据仓库）中的新增功能
查看 Microsoft 分析平台系统 （APS） 的最新设备更新中的新增功能。 APS 是托管 MPP SQL Server 并行数据仓库的横向扩展本地设备。 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.6"></a>
## <a name="aps-cu76"></a>APS CU7.6
发布日期 - 2020 年 4 月

### <a name="rename-column"></a>重命名列
升级到 CU7.6 后，客户将能够重命名用户创建的表的列。 有关语法、示例、限制和详细信息，请参阅[RENAME（转用 SQL）。](https://docs.microsoft.com/sql/t-sql/statements/rename-transact-sql)

### <a name="alter-view"></a>更改视图
客户现在将能够更改视图。 有关详细信息，请参阅[ALTER 视图（转用 SQL）。](https://docs.microsoft.com/sql/t-sql/statements/alter-view-transact-sql)

<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
发布日期 - 2019 年 9 月

### <a name="alter-external-data-source"></a>更改外部数据源
客户将能够使用 CU7.5 更新更改外部数据源定义。 具有 Hadoop 名称节点高可用性的客户现在可以更改数据源，以在发生故障转移时更改参数。 对于 APS，只能更改位置、RESOURCE_MANAGER_LOCATION和凭据。 有关详细信息，请参阅[更改外部数据源](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017)。

### <a name="cdh-515-and-516-support-with-polybase"></a>CDH 5.15 和 5.16 支持 PolyBase
具有 CU7.5 更新的 APS 上的 PolyBase 现在支持来自 Cloudera 的 CDH 5.15 和 5.16 版本的 Hadoop 发行版。 对 CDH 5.x 版本使用选项 6。 

### <a name="try_convert-and-try_cast-support"></a>Try_Convert和Try_Cast支持
CU7.5 APS 现在支持[TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017)和[tsql函数TRY_CONVERT。](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) 如果转换成功，这两个函数都将返回转换为指定数据类型的值;否则，返回 null。

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
发布日期 - 2019 年 5 月

### <a name="loading-large-rows-with-dwloader"></a>使用 dwloader 加载大型行
从 APS CU7.4 开始，客户将能够使用新的 dwloader 将行加载到大于 32 KB（32，768 字节）的表中。 新的 dwloader 支持 -l 开关，该开关采用 32768 和 33554432（以字节为单位）之间的整数值来加载大于 32 KB 的行。 仅当加载大型行（大于 32 KB）时才使用此选项，因为此交换机将在客户端和服务器上分配更多内存，并可能降低负载。 你可以从[下载网站](https://www.microsoft.com/download/details.aspx?id=57472)下载新的dwloader。  

### <a name="hdp-30-and-31-support-with-polybase"></a>使用 PolyBase 支持 HDP 3.0 和 3.1
APS 上的 PolyBase 现在支持 HDP 3.0 和 3.1 此更新。 对 HDP 3.x 版本使用选项 7。 有关详细信息，请参阅[PolyBase 连接](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql)页。

### <a name="utf16-file-support-with-polybase"></a>UTF16 文件支持与 PolyBase
PolyBase 现在支持读取 UTF16 （LE） 编码中分隔的文本文件。 有关设置详细信息，请参阅[创建外部文件格式](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql)。 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
发布日期 - 2018 年 12 月

### <a name="common-subexpression-elimination"></a>常见子表达式清除
APS CU7.3 通过在 SQL 查询优化器中消除常见子表达式来提高查询性能。 改进以两种方式改进查询。 第一个好处是能够识别和消除此类表达式，这有助于缩短 SQL 编译时间。 第二个更重要的好处是消除了这些冗余子表达式的数据移动操作，从而加快了查询的执行时间。 有关此功能的详细说明，请参阅[此处](common-sub-expression-elimination.md)。

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>APS 信息学连接器 Informatica 10.2.0 发布
我们发布了适用于 Informatica 版本 10.2.0 和 10.2.0 修补程序 1 的 APS 的新版本 Informatica 连接器。 新的连接器可以从[下载站点](https://www.microsoft.com/download/details.aspx?id=57472)下载。

#### <a name="supported-versions"></a>支持的版本

| APS 版本 | Informatica PowerCenter | 驱动程序 |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL 服务器本机客户端 11.x |
| APS 2016 及更高版本 | 10.2.0， 10.2.0 修补程序 1 | SQL 服务器本机客户端 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
发布日期 - 2018 年 10 月

### <a name="support-for-tls-12"></a>支持 TLS 1.2
APS CU7.2 支持 TLS 1.2。 客户端计算机到 APS 和 APS 节点内通信现在只能设置为通过 TLS1.2 进行通信。 安装在客户端计算机上（设置为仅通过 TLS 1.2 进行通信）的 SSDT、SSIS 和 Dwloader 等工具现在可以使用 TLS 1.2 连接到 APS。 默认情况下，APS 将支持所有 TLS（1.0、1.1 和 1.2）版本，以便向后兼容。 如果您希望将 APS 设备设置为严格使用 TLS 1.2，则可以通过更改注册表设置来执行此操作。 

有关详细信息，请参阅在[APS 上配置 TLS1.2。](configure-tls12-aps.md)

### <a name="hadoop-encryption-zone-support-for-polybase"></a>对 PolyBase 的 Hadoop 加密区域支持
PolyBase 现在可以与 Hadoop 加密区域进行通信。 请参阅[配置 Hadoop 安全性](polybase-configure-hadoop-security.md#encryptionzone)中所需的 APS 配置更改。

### <a name="insert-select-maxdop-options"></a>插入-选择最大多普选项
我们添加了一个[功能开关](appliance-feature-switch.md)，允许您选择大于 1 的 maxdop 设置，用于插入选择操作。 现在，您可以将 maxdop 设置设置为 0、1、2 或 4。 默认值为 1。

> [!IMPORTANT]  
> 增加 maxdop 有时可能会导致操作速度较慢或死锁错误。 如果发生这种情况，请将设置更改回 maxdop 1 并重试该操作。

### <a name="columnstore-index-health-dmv"></a>列存储索引运行状况 DMV
您可以使用**dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv 查看列存储索引运行状况信息。 使用以下视图确定碎片并决定何时重新生成或重新组织列存储索引。

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[pdw_node_id]    = nt.[pdw_node_id]                                          
)
select *
from cte;
```

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>ORC 和 Parquet 文件的 PolyBase 日期范围增加
使用 PolyBase 读取、导入和导出日期数据类型现在支持 ORC 和 Parquet 文件类型的 1970-01-01 和 2038-01-20 之后的日期。

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>SQL Server 2017 的 SSIS 目标适配器作为目标
新的APS SSIS目标适配器，支持SQL Server 2017作为部署目标可以从[下载站点](https://www.microsoft.com/download/details.aspx?id=57472)下载。

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
发布日期 - 2018 年 7 月

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>DBCC 命令不消耗并发槽（行为更改）
APS 支持 T-SQL [DBCC 命令](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql)的子集，如[DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)。 以前，这些命令会占用[并发插槽](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots)，从而减少了可以执行的用户加载/查询数。 这些`DBCC`命令现在在本地队列中运行，这些队列不使用用户并发槽来提高整体查询执行性能。

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>将某些元数据调用替换为目录对象
将目录对象用于元数据调用而不是使用 SMO 在 APS 中显示了性能改进。 从 CU7.1 开始，这些元数据调用中的一些默认使用目录对象。 如果使用元数据查询的客户遇到任何问题，则[功能切换](appliance-feature-switch.md)可以关闭此行为。

### <a name="bug-fixes"></a>Bug 修复
我们已升级到 SQL Server 2016 SP2 CU2 与 APS CU7.1。 升级修复了下面描述的一些问题。

| Title | 描述 |
|:---|:---|
| **潜在的元组前锁死** |升级修复了分布式事务和元组器后台线程中长期存在的死锁的可能性。 安装 CU7.1 后，使用 TF634 停止元组器作为 SQL Server 启动参数或全局跟踪标志的客户可以安全地将其删除。 | 
| **某些延迟/潜在顾客查询失败** |对于具有嵌套滞后/潜在顾客函数的 CCI 表的某些查询，这些查询会出错，现在通过此升级修复了这些查询。 | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
发布日期 - 2018 年 5 月

APS 2016 是升级到 AU7 的先决条件。 以下是 APS AU7 中的新功能：

### <a name="auto-create-and-auto-update-statistics"></a>自动创建和自动更新统计信息
默认情况下，APS AU7 会自动创建和更新统计信息。 要更新统计信息设置，管理员可以使用[配置管理器](appliance-configuration.md#CMTasks)中的新功能切换菜单项。 [要素开关](appliance-feature-switch.md)控制统计信息的自动创建、自动更新和异步更新行为。 您还可以使用[ALTER 数据库（并行数据仓库）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)语句更新统计信息设置。

### <a name="t-sql"></a>T-SQL
现在@var支持选择。 有关详细信息，请参阅[选择局部变量](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

查询提示 HASH 和 ORDER 组现在受支持。 有关详细信息，请参阅[提示（转算 SQL） - 查询](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>功能开关
APS AU7 在[配置管理器](launch-the-configuration-manager.md)中引入了功能切换。 启用自动统计和 DmsProcessStopMessageTimeoutIn，现在它们是可配置的选项，管理员可以更改这些选项。

### <a name="known-issues"></a>已知问题
使用 APS AU7 软件，提供了英特尔 BIOS 更新，修复了被描述为*投机性执行侧通道攻击*的问题。 攻击的目的是利用所谓的*幽灵和熔毁漏洞*。 尽管与 APS 一起打包，但 BIOS 更新是手动安装的，而不是作为 APS AU7 软件安装的一部分。

微软建议所有客户安装更新的 BIOS。 Microsoft 已测量内核虚拟地址阴影 （KVAS）、内核页表间接 （KPTI） 和间接分支预测缓解 （IBP） 对各种环境中各种 SQL 工作负载的影响。 测量发现某些工作负载显著退化。 根据结果，建议在生产环境中部署 BIOS 更新之前测试启用 BIOS 更新的性能效果。 [在此处](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)查看 SQL Server 指南。

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
本节介绍了 APS 2016-AU6 的新功能。

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 在最新的 SQL Server 2016 版本上运行，并使用默认数据库兼容性级别 130。 SQL Server 2016 支持新功能，例如：

- 群集列存储索引的辅助索引。
- 多基的 Kerberos。

### <a name="t-sql"></a>T-SQL
APS AU6 支持这些 T-SQL 兼容性改进。  这些附加语言元素使从 SQL Server 和其他数据源迁移变得更加容易。 

- 除了 Windows 排序规则之外，现在还支持[列级 SQL 排序规则][]。
- [群集列存储索引上的非群集索引][]可提高搜索群集列存储索引中特定值的查询的性能。 
- [SELECT...INTO][] 
- [sp_spaceused（）][]显示表或数据库中使用或保留的磁盘空间。
- [宽表][]支持与 SQL Server 2016 相同。 行大小的前一个限制为 32 K 不再存在。 

**数据类型**

- [瓦尔查尔（最大值][][）、NVARCHAR（MAX）][]和[瓦尔里卡（MAX）。][] 这些 LOB 数据类型的最大大小为 2 GB。 要加载这些对象，请使用[bcp 实用程序][]。 PolyBase 和 dwloader 当前不支持这些数据类型。 
- [SYS名称][]
- [唯一标识符][]
- [数字][]和 DECIMAL 数据类型。

**开窗函数**

- SELECT 语句 OVER 子句中的[行或范围][]。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**安全功能**

- [CHECKSUM（）][]和[BINARY_CHECKSUM（）][]
- [HAS_PERMS_BY_NAME（）][]

**其他功能**

- [纽ID（）][]
- [兰德（）][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 增强功能

- 与霍顿工程 HDP 2.4 和 HDP 2.5 兼容
- 通过数据库作用域凭据支持 Kerberos
- 使用 Azure 存储 Blob 提供凭据支持

### <a name="install-and-upgrade-enhancements"></a>安装和升级增强功能

**企业体系结构更新**将现有设备升级到 APS AU6 可安装最新的固件和驱动程序更新，其中包括安全修补程序。 

HPE 或 DELL 的新设备包括所有最新更新以及：

- 最新一代处理器支持（布罗德韦尔）
- 更新至 DDR4 DIMM
- 改进的 DIMM 吞吐量

**集成**

- 完全限定的域名 （FQDN） 支持使得可以设置对设备的域信任。 
- 要使用 FQDN，您需要在升级期间执行完全升级并选择加入。 

**减少停机时间**安装或升级到 APS AU6 的速度更快，并且需要的停机时间比以前的版本要少。 为了减少停机时间，安装或升级： 

 - 使用包含所有更新的映像在 2016 年 6 月内简化应用 WSUS 更新
 - 使用驱动程序和固件更新应用安全更新
 - 将最新的修补程序和产品验证实用程序 （PAV） 放在设备上，以便无需下载即可安装。

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[列级 SQL 排序规则]: ~/relational-databases/collations/collation-and-unicode-support.md

[群集列存储索引上的非群集索引]:/sql/t-sql/statements/create-index-transact-sql
[瓦尔查尔（最大）]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[恩瓦尔查尔（最大）]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[瓦里卡（最大）]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYS名称]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused（）]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[宽桌]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp 实用工具]:/sql/tools/bcp-utility
[唯一标识符]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[数字]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[行或范围]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[校验（）]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM（）]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME（）]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[纽ID（）]:/sql/t-sql/functions/newid-transact-sql
[兰德（）]:/sql/t-sql/functions/rand-transact-sql


  

  


