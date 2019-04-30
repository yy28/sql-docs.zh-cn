---
title: 什么是分析平台系统-向外缩放数据仓库中的新增功能
description: 请参阅什么是 Microsoft Analytics Platform System 承载 MPP SQL Server 并行数据仓库的横向扩展的本地设备中的新增功能。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cc64fdd430e64f7ad1b152234c2a203f453745c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243780"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>什么是横向扩展 MPP 数据仓库的分析平台系统中的新增功能
请参阅什么是最新的设备更新为 Microsoft Analytics Platform System (APS) 中的新增功能。 APS 是承载 MPP SQL Server 并行数据仓库的横向扩展的本地设备。 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
发布日期-2018 年 12 月

### <a name="common-subexpression-elimination"></a>常见子表达式清除
APS CU7.3 可以提高查询性能与在 SQL 查询优化器的公用子表达式消除。 改进提高了两种方法中的查询。 第一个好处是可以识别并消除此类表达式帮助减少 SQL 编译时间。 第二个和更重要的好处是这些冗余的子表达式的数据移动操作将消除因此执行时间的查询变得更快。 可以找到此功能的详细的说明[此处](common-sub-expression-elimination.md)。

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>对于 Informatica 10.2.0 APS Informatica 连接器已发布
我们发布了有关 APS Informatica 10.2.0 和 10.2.0 版本使用 Informatica 连接器的新版本修补程序 1。 可以从下载新连接器[下载站点](https://www.microsoft.com/download/details.aspx?id=57472)。

#### <a name="supported-versions"></a>支持的版本

| APS 版本 | Informatica PowerCenter | 驱动程序 |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 和更高版本 | 10.2.0、 10.2.0 修补程序 1 | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
发布日期-2018 年 10 月

### <a name="support-for-tls-12"></a>支持 TLS 1.2
APS CU7.2 支持 TLS 1.2。 客户端计算机到 APS 和 APS 节点内部进行通信可以立即被设置为仅通过 TLS1.2 进行通信。 SSDT、 SSIS 和 Dwloader 设置为仅通过 TLS 1.2 进行通信的客户端计算机上安装了之类的工具现在可以连接到 AP 使用 TLS 1.2。 默认情况下，AP 将支持 TLS （1.0、 1.1 和 1.2） 的所有版本的向后兼容性。 如果你想要设置 APS 设备为严格使用 TLS 1.2，您可以为此更改注册表设置。 

有关详细信息，请参阅[AP 上配置 TLS1.2](configure-tls12-aps.md)。

### <a name="hadoop-encryption-zone-support-for-polybase"></a>为 PolyBase 支持 Hadoop 加密区域
PolyBase 现在可以进行通信到 Hadoop 加密区域。 请参阅 APS 中所需的配置更改[配置的 Hadoop 安全性](polybase-configure-hadoop-security.md#encryptionzone)。

### <a name="insert-select-maxdop-options"></a>Insert Select maxdop 选项
我们添加了[功能开关](appliance-feature-switch.md)，可以选取大于 1 的 insert select 操作的 maxdop 设置。 现在，可以设置 maxdop 设置为 0、 1、 2 或 4。 默认值为 1。

> [!IMPORTANT]  
> 增加 maxdop 有时可能会较慢的操作或死锁错误导致。 如果发生这种情况，将设置更改回 maxdop 1，重试该操作。

### <a name="columnstore-index-health-dmv"></a>列存储索引运行状况 DMV
您可以查看列存储索引运行状况信息使用**dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv。 使用以下视图来确定碎片并决定何时重新生成或重新组织列存储索引。

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

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>PolyBase 适用于 ORC 和 Parquet 文件的日期范围增加
读取、 导入和导出现在使用 PolyBase 的日期数据类型支持 ORC 和 Parquet 文件类型日期 1970年-01-01 之前和之后 2038年-01-20。

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>为目标的 SQL Server 2017 的 SSIS 目标适配器
支持 SQL Server 2017，作为部署目标可以从下载的新 APS SSIS 目标适配器[下载站点](https://www.microsoft.com/download/details.aspx?id=57472)。

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
发布日期-2018 年 7 月

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>DBCC 命令不会消耗并发槽位 （行为更改）
APS 支持 T-SQL 子集[DBCC 命令](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql)如[DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)。 以前，这些命令将占用[并发槽](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots)减少的用户负载/查询无法执行。 `DBCC`命令现在运行在不使用用户并发槽提高总体查询执行性能的本地队列中。

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>某些元数据的调用替换为目录对象
使用目录对象的元数据调用，而不是使用 SMO 有 APS 中显示性能改进。 从 CU7.1 开始，某些元数据调用现在目录对象默认情况下使用。 可以通过关闭此行为[功能开关](appliance-feature-switch.md)如果使用元数据查询的客户遇到任何问题。

### <a name="bug-fixes"></a>Bug 修复
我们已升级到 SQL Server 2016 SP2 CU2 APS CU7.1 使用。 升级解决了如下所述的一些问题。

| 标题 | Description |
|:---|:---|
| **潜在的元组搬运者进程死锁** |升级分布式事务和元组发动机后台线程中修复，长期的合作可能导致死锁。 在安装后 CU7.1，TF634 用于停止为 SQL Server 启动参数或全局跟踪标志的元组发动机的客户可以放心删除它。 | 
| **某些 lag/lead 查询失败** |将错误的嵌套的 lag/lead 函数使用 CCI 表的某些查询现已修复此升级。 | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
发布日期-2018 年 5 月

APS 2016 后，才可以升级到 AU7。 APS AU7 中的新增功能如下：

### <a name="auto-create-and-auto-update-statistics"></a>自动创建和自动更新统计信息
APS AU7 创建，并默认情况下将自动更新统计信息。 若要更新统计信息设置，管理员可以使用中的新功能切换菜单项[Configuration Manager](appliance-configuration.md#CMTasks)。 [功能开关](appliance-feature-switch.md)控制不符、 自动更新和异步更新统计信息的行为。 此外可以更新使用的统计信息设置[ALTER DATABASE （并行数据仓库）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)语句。

### <a name="t-sql"></a>T-SQL
选择@var现在支持。 有关详细信息，请参阅[选择本地变量](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

现在支持哈希和 ORDER GROUP 查询提示。 有关详细信息，请参阅[Hints(Transact-SQL)-查询](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>功能开关
APS AU7 引入了中的功能切换[Configuration Manager](launch-the-configuration-manager.md)。 AutoStatsEnabled 和 DmsProcessStopMessageTimeoutInSeconds 现在都可以由管理员更改的可配置选项。

### <a name="known-issues"></a>已知问题
APS AU7 软件还修复了描述为问题提供 Intel BIOS 更新*推理执行旁道攻击*。 攻击的目标是利用所谓*Spectre 和 Meltdown 漏洞*。 尽管与 APS 一起打包，手动安装 BIOS 更新而不是作为 APS AU7 软件安装的一部分。

Microsoft 建议所有客户，若要安装更新 BIOS。 Microsoft 已在各种环境中的各种 SQL 工作负荷上测量内核虚拟地址隐藏 (KVAS)、 内核页表间接寻址 (KPTI) 和间接分支预测缓解措施 (IBP) 的效果。 度量值上某些工作负荷找到显著下降。 根据结果，建议是测试对性能产生影响的生产环境中部署之前启用 BIOS 更新。 请参阅 SQL Server 指南[此处](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)。

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
本部分针对 APS 2016 AU6 所述的新功能。

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 上最新的 SQL Server 2016 版本中，在运行，并使用默认数据库的兼容性级别 130。 SQL Server 2016 支持等新功能：

- 聚集列存储索引的辅助索引。
- Polybase Kerberos。

### <a name="t-sql"></a>T-SQL
APS AU6 支持这些 T-SQL 的兼容性改进。  这些其他语言元素，使其更轻松地从 SQL Server 和其他数据源迁移。 

- [列级 SQL 排序规则][]现在还支持，除了 Windows 排序规则。
- [聚集列存储索引的非聚集索引][]改进搜索聚集列存储索引中的特定值的查询的性能。 
- [SELECT...INTO][] 
- [sp_spaceused()][]显示的磁盘空间使用或保留的表或数据库中。
- [宽表][]支持是 SQL Server 2016 相同。 32k 的行大小的上一限制不再存在。 

**数据类型**

- [VARCHAR(MAX)][]， [NVARCHAR(MAX)][]并[VARBINARY(MAX)][]。 这些 LOB 数据类型具有的最大大小为 2 GB。 若要加载这些对象，请使用[bcp Utility][]。 PolyBase 和 dwloader 当前不支持这些数据类型。 
- [SYSNAME][]
- [唯一标识符][]
- [NUMERIC][]和 DECIMAL 数据类型。

**开窗函数**

- [ROWS 或 RANGE][] OVER 子句的 SELECT 语句中。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**安全函数**

- [CHECKSUM()][]和[BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**其他函数**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 增强功能

- 与的 Hortonworks HDP 2.4 和 HDP 2.5 兼容性
- Kerberos 支持通过数据库范围凭据
- 使用 Azure 存储 Blob 的凭据支持

### <a name="install-and-upgrade-enhancements"></a>安装和升级增强功能

**企业体系结构更新**到 AP AU6 升级你现有的设备安装最新的固件和驱动程序更新，其中包括安全修补程序。 

新的设备从 HPE 或 DELL 包括所有最新的更新以及：

- 最新生成处理器支持 (Broadwell)
- 更新到采用 DDR4 Dimm
- 改进了的 DIMM 吞吐量

**集成**

- 完全限定域名 (FQDN) 的支持使可能安装到设备的域信任。 
- 若要使用 FQDN，您需要执行完全升级并且选择在升级过程。 

**减少了停机时间**安装或升级到 AP AU6 更快，且需要较少的停机时间比以前的版本。 若要降低停机时间、 安装或升级： 

 - 简化通过使用包含截至 2016 年 6 月的所有更新的映像应用 WSUS 更新
 - 应用安全更新的驱动程序和固件更新
 - 将最新修补程序和设备验证实用程序 (PAV) 置于你的设备这样他们就可以使用无需在下载之后进行安装。

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[列级 SQL 排序规则]: ~/relational-databases/collations/collation-and-unicode-support.md

[聚集列存储索引的非聚集索引]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[宽表]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp Utility]:/sql/tools/bcp-utility
[唯一标识符]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[NUMERIC]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[ROWS 或 RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


