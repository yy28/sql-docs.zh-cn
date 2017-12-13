---
title: "已更新 - 关系数据库文档 | Microsoft Docs"
description: "显示关系数据库文档中最近更改的更新内容片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 1fbc7affa833eb34b6e13e28b229d47ac0b05a5c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新文章和最近更新的文章：关系数据库文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：从 2017-09-28 到 2017-12-02&nbsp;&nbsp;&nbsp;
- 主题领域：&nbsp; 关系数据库。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [使用 SSMS XEvent Profiler](extended-events/use-the-ssms-xe-profiler.md)
2. [将平面文件导入 SQL 向导](import-export/import-flat-file-wizard.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [tempdb 数据库](#TitleNum_1)
2. [内存管理体系结构指南](#TitleNum_2)
3. [统计信息](#TitleNum_3)
4. [sp_server_diagnostics (Transact-SQL)](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>1.&nbsp;[tempdb 数据库](databases/tempdb-database.md)

更新日期：2017-11-20 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[下一篇](#TitleNum_2)）

<!-- Source markdown line 121.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c8bb5f9c40625aaf955295e5b5d03e4257e6c6b 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d  (PR=4039  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=ef1fa818beea435f58986af3379853dc28f5efd8) -->



**优化 tempdb 性能**

 tempdb 数据库的大小和物理位置可能会影响系统的性能。 例如，如果为 tempdb 定义的大小过小，则每次重启 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 实例时，都可能会占用部分系统处理负荷，以使 tempdb 自动增长到支持工作负荷所需的大小。

 如有可能，请使用 [database instant file initialization--../../relational-databases/databases/database-instant-file-initialization.md) 改进数据文件增长操作的性能。

 通过将文件大小设置为足够容纳环境中典型工作负荷的值来预分配所有 tempdb 文件的空间。 这可以避免 tempdb 因扩展得过于频繁而影响性能。 tempdb 数据库应设置为自动增长，但是在出现意外情况时此设置将用于增加磁盘空间。

 每个 [filegroup--../../relational-databases/databases/database-files-and-filegroups.md#filegroups) 中的数据文件应大小一致，因为 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 使用比例填充算法，这种算法优先在拥有更多可用空间的文件中进行分配。 将 tempdb 分割成大小相等的多个数据文件，可以为使用 tempdb 的操作提供更高的并行效率。

 将文件增量设置为合理的大小以避免 tempdb 数据库文件的增量过小。 如果文件的增量与写入 tempdb 的数据量相比过小，则 tempdb 可能需要不断扩大。 这将影响性能。

 要检查当前 tempdb 大小和增长参数，请使用以下查询：
```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeinMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-memory-management-architecture-guidememory-management-architecture-guidemd"></a>2.&nbsp;[内存管理体系结构指南](memory-management-architecture-guide.md)

更新日期：2017-11-28 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_1) | [下一篇](#TitleNum_3)）

<!-- Source markdown line 75.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 dd47431ca47eab16af40e41adaeeaf3fc5fb7461 445f013af3bdad65dd3eaf837db7f744b43e8f97  (PR=4113  ,  Filename=memory-management-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



在 SQL Server (..!NCLUDE-NotShown--ssVersion2005--../includes/ssversion2005-md.md)]、..!NCLUDE-NotShown--ssKatmai--../includes/ssKatmai-md.md)] 和 ..!NCLUDE-NotShown--ssKilimanjaro--../includes/ssKilimanjaro-md.md)]) 的早期版本中，使用五种不同的机制分配内存：
-  **单页分配器 (SPA)**，它仅包含 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 进程中小于或等于 8 KB 的内存分配。 “max server memory (MB)”和“min server memory (MB)”这两个配置选项确定 SPA 消耗的物理内存的限制。 同时，缓冲池也是用于 SPA 的机制，并且还是最大的单页分配使用者。
-  **多页分配器 (MPA)**，用于需要 8 KB 以上的内存分配。
-  **CLR 分配器**，包含 CLR 初始化期间创建的 SQL CLR 堆及其全局分配。
-  用于 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 进程中 [thread stacks--../relational-databases/memory-management-architecture-guide.md#stacksizes) 的内存分配。
-  **直接 Windows 分配 (DWA)**，用于直接向 windows 进行的内存分配请求。 包括由加载到 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 进程中的模块使用 Windows 堆和直接进行虚拟分配。 此类内存分配请求的示例包括从扩展存储过程 DLL 分配、使用自动化过程（sp_OA 调用）创建的对象以及从链接服务器提供程序分配。

从 ..!NCLUDE-NotShown--ssSQL11--../includes/sssql11-md.md)] 开始，单页分配、多页分配和 CLR 分配全部合并到“任意大小”页分配器中，受到由“最大服务器内存(MB)”和“最小服务器内存(MB)”配置选项控制的内存限制。 此更改使通过 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 内存管理器的所有内存要求能更准确地调整大小。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-statisticsstatisticsstatisticsmd"></a>3.&nbsp;[统计信息](statistics/statistics.md)

更新日期：2017-11-27 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_2) | [下一篇](#TitleNum_4)）

<!-- Source markdown line 48.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1dbe3bd6fdfcd27cf4a597cac5a4a09821b51ba7 971cfccf75fbc8842a0ef020a2bc93992c5f4ad9  (PR=4087  ,  Filename=statistics.md  ,  Dirpath=docs\relational-databases\statistics\  ,  MergeCommitSha40=9fbe5403e902eb996bab0b1285cdade281c1cb16) -->



> [!NOTE]
> ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 中的直方图仅为统计信息对象的键列集中第一个 columnΓÇöthe 列生成。

若要创建直方图，查询优化器将对列值进行排序，计算与每个非重复列值匹配的值数，然后将列值聚合到最多 200 个连续直方图梯级中。 每个直方图梯级都包含一个列值范围，后跟上限列值。 该范围包括介于两个边界值之间的所有可能列值，但不包括边界值自身。 最小排序列值是第一个直方图梯级的上限值。

下文详细介绍了 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 如何通过三个步骤从已排序的列值集创建直方图：

- **直方图初始化**：在第一步中，处理始于排序集开始处的一个值序列，并收集 range_high_key、equal_rows、range_rows 和 distinct_range_rows 的最多 200 个值（在此步骤中，range_rows 和 distinct_range_rows 始终为零）。 已用尽所有输入或已找到 200 个值时，结束第一步。
- **使用 Bucket 合并进行扫描**：第二步中，按排序顺序处理从统计信息键前导列算起的每个额外值；将每个相继值添加到最后一个范围或在末尾创建一个新范围（这可能是因输入值已排序所致）。 如果创建了一个新范围，则一对现有相邻范围折叠为单个范围。 选择这对范围以最大限度减少信息丢失。 此方法使用最大差异算法使直方图中的梯级数减至最少，并同时最大化边界值之间的差异。 折叠后，梯级数在整个步骤中保持为 200。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-spserverdiagnostics-transact-sqlsystem-stored-proceduressp-server-diagnostics-transact-sqlmd"></a>4.&nbsp;[sp_server_diagnostics (Transact-SQL)](system-stored-procedures/sp-server-diagnostics-transact-sql.md)

更新日期：2017-11-21 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_3)）

<!-- Source markdown line 157.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d0d97efbb0b16638d0120af9ac5e66ec3bcfa391 b98735ec26a091f8c8c58ca1790243be7942e038  (PR=4052  ,  Filename=sp-server-diagnostics-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=45e4efb7aa828578fe9eb7743a1a3526da719555) -->



下面的示例查询读取表格的摘要输出：
```sql
SELECT create_time,
       component_name,
       state_desc
FROM SpServerDiagnosticsResult;
```

下面的示例查询读取表格中每个组件的部分详细输出：
```sql
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult
where component_name like 'resource'
go

-- Nonpreemptive waits
```







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (3+14)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新的和更新的文章 (1+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)
- [新文章和更新的文章 (87+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章和更新的文章 (5+4)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (0+1)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新文章和更新的文章 (2+2)：SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)
- [新文章和更新的文章 (10+9)：Linux 版 SQL 文档](../linux/new-updated-linux.md)
- [新文章和更新的文章 (2+4)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新文章和更新的文章 (4+2)：SQL Reporting Services 文档](../reporting-services/new-updated-reporting-services.md)
- [新文章和更新的文章 (0+1)：SQL 示例文档](../sample/new-updated-sample.md)
- [新文章和更新的文章 (21+0)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章和更新的文章 (5+1)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+1)：SQL Server Data Tool (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新文章和更新的文章 (1+0)：SQL Server 迁移助手 (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新文章和更新的文章 (0+0)：SQL 数据迁移助手 (DMA) 文档](../dma/new-updated-dma.md)
- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新文章和更新的文章 (0+0)：SQL 工具文档](../tools/new-updated-tools.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


