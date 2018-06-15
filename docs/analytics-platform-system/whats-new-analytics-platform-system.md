---
title: 什么是分析平台系统 – 向外扩展数据仓库中的新增功能
description: 请参阅什么是 Microsoft® 分析平台系统中的新增、 横向扩展本地承载 MPP SQL Server 并行数据仓库的设备。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c2408e84e7ff81f54ad00a98f85cd8dce7b04131
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2018
ms.locfileid: "34550638"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>什么是分析平台系统向外扩展 MPP 数据仓库中的新增功能
请参阅什么是最新设备更新的 Microsoft® 分析平台系统 (AP) 中的新增功能。 AP 是承载 MPP SQL Server 并行数据仓库的横向扩展本地设备。 


## <a name="aps-au7"></a>AP AU7
APS2016 是要升级到 AU7 的先决条件。 以下是用于 AP AU7 的新增功能：

### <a name="auto-create-and-auto-update-statistics"></a>自动创建，并自动更新统计信息
AP AU7 创建，并且默认情况下，自动更新统计信息。 若要更新统计信息设置，管理员可以使用中的新功能交换机菜单项[Configuration Manager](appliance-configuration.md#CMTasks)。 [功能开关](appliance-feature-switch.md)控制不符，自动更新，以及异步更新统计信息的行为。 你还可以更新统计信息设置[ALTER DATABASE （并行数据仓库）](/sql/t-sql/statements/alter-database-parallel-data-warehouse)语句。

### <a name="t-sql"></a>T-SQL
选择@var现在支持。 有关详细信息，请参阅 [选择本地变量] （/ sql/t-sql/language-elements/select-local-variable-transact-sql） 

现在支持查询提示哈希和顺序组。 有关详细信息，请参阅 [Hints(Transact-SQL)-查询] （/sql/t-sql/查询/提示-transact-sql 的查询）

### <a name="feature-switch"></a>功能开关
AP AU7 引入了中的功能开关[Configuration Manager](launch-the-configuration-manager.md)。 AutoStatsEnabled 以及 DmsProcessStopMessageTimeoutInSeconds 现可以由管理员更改的可配置选项。

### <a name="known-issues"></a>已知问题
AP AU7 软件，我们是打包提供 （又修复"推测执行边信道攻击"Intel BIOS 更新。 Spectre 和垮台漏洞）。 通过打包在一起，BIOS 更新手动安装并不是 AP AU7 软件的一部分安装。 Microsoft 建议所有客户进行安装，BIOS 更新。 Microsoft 已测量内核虚拟地址隐藏 (KVAS)、 内核页表间接寻址 (KPTI) 和间接分支预测缓解 (IBP) 不同的环境中的各种 SQL 工作负荷的影响，并且在某些上发现大幅度降低工作负荷。 我们建议你测试对性能产生影响的生产环境中部署它们之前启用 BIOS 更新。 如果启用这些功能的性能效果是太高，现有的应用程序，可以考虑是否隔离运行的不受信任代码中你 AP 的设备是更好的防范应用程序。 请参阅 SQL Server 指南[此处](https://support.microsoft.com/en-us/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)。

## <a name="aps-2016"></a>AP 2016
这些是用于 AP 2016 的新增功能：

### <a name="sql-server-2016"></a>SQL Server 2016

AP 2016 在最新的 SQL Server 2016 版本上运行，并使用默认数据库兼容性级别 130。  SQL Server 2016 使可以为 PolyBase 支持的一些新功能，例如辅助索引的聚集列存储索引和 Kerberos。 


### <a name="t-sql"></a>T-SQL
AP 2016 支持这些 T-SQL 兼容性改进。  这些其他语言元素更加轻松地从 SQL Server 和其他数据源迁移。 

- [列级 SQL 排序规则][]现在支持除了 Windows 排序规则。
- [聚集列存储索引的非聚集索引][]改进搜索聚集列存储索引中的特定值的查询性能。 
- [选择...到][] 
- [sp_spaceused()][]显示磁盘空间使用，或保留表或数据库中。
- [宽表][]支持等同于 SQL Server 2016。 行大小以前限制为 32k 不再存在。 

**数据类型**

- [VARCHAR(MAX)][]， [NVARCHAR(MAX)][]和[varbinary （max)][]。 这些 LOB 数据类型的最大为 2 GB。 若要加载这些对象，请使用[bcp Utility][]。 Polybase 和 dwloader 当前不支持这些数据类型。 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMERIC][]和十进制数据类型。

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

- 与 Hortonworks HDP 2.4 和 HDP 2.5 兼容性
- Kerberos 支持通过数据库范围凭据
- Azure 存储 blob 的凭据支持

### <a name="install-and-upgrade-enhancements"></a>安装和升级的增强功能

**企业体系结构更新**到 AP 2016 升级你现有的设备安装最新的固件和驱动程序更新，包括安全修补程序。 

一个新的设备从 HPE 或 DELL 包括所有最新的更新以及：

- 最新生成处理器支持 (Broadwell)
- 更新到 DDR4 Dimm
- 改进了的 DIMM 吞吐量

**集成**

- 完全限定域名 (FQDN) 支持使可以安装到设备的域信任。 
- 若要使用 FQDN，你需要执行完整的升级，并选择在升级过程。 

**减少了停机时间**安装或升级到 AP 2016 速度更快，并且需要比以前的版本中减去停机时间。 若要降低停机时间、 安装或升级： 

 - 通过使用包含通过 2016 年 6 月的所有更新的映像应用 WSUS 更新的优化
 - 适用的驱动程序和固件更新的安全更新
 - 这样便已准备好安装，也无需下载它们会在你的设备上的最新修补程序和设备验证实用程序 (PAV)。


<!--MSDN references-->
[database compatibility level 130]:/sql/t-sql/statements/alter-database-transact-sql-compatibility-level
[列级 SQL 排序规则]:/sql/relational-databases/collations/collation-and-unicode-support
[聚集列存储索引的非聚集索引]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY （MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[选择...到]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[宽表]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp Utility]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
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


  

  


