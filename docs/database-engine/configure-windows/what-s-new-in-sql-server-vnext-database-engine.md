---
title: "SQL Server vNext（数据库引擎）中的新增功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# SQL Server vNext（数据库引擎）中的新增功能
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

**注意：**SQL Server vNext 还包括 SQL Server 2016 Service Pack 中新增的功能。 有关这些项目，请参阅 [SQL Server 2016（数据库引擎）中的新增功能](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)。

## <a name="sql-server-database-engine-ctp-13"></a>SQL Server 数据库引擎 (CTP 1.3)
- 间接检查点性能改进。
- 新增了对“无群集可用性组”的支持。
- 添加了“最小复制提交可用性组”设置。
- 可用性组现可跨 Windows-Linux 工作，从而实现跨操作系统的迁移和测试。
- 新增了对“临时表保留策略”的支持，
- New DMV SYS.DM_DB_STATS_HISTOGRAM
- 新增了对联机非聚集列存储索引生成和重新生成的支持
- 5 个新的动态管理视图，可返回有关 Linux 进程的信息。 有关详细信息，请参阅 [Linux 进程动态管理视图](../../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)。   
- 添加了 [sys.dm_db_stats_histogram (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)，用于检查统计信息。

## <a name="sql-server-database-engine-ctp-12"></a>SQL Server 数据库引擎 (CTP 1.2)

- 随 SQL Server Management Studio 版本 16.4 发布的数据库优化顾问 (DTA)，在分析 SQL Server 2016 及更高版本时，具有额外的选项。    
   - 改进的性能。 有关详细信息，请参阅[使用数据库引擎优化顾问 (DTA) 改进性能的建议](../../relational-databases/performance/performance-improvements-using-dta-recommendations.md)。
   - `-fc` 选项，可允许建议列存储索引。 有关详细信息，请参阅 [DTA 实用工具](../../tools/dta/dta-utility.md)和[数据引擎优化顾问 (DAT) 中的列存储索引建议](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)。  
   - `-iq` 选项，可允许 DTA 从查询存储中查看工作负载。 有关详细信息，请参阅[使用查询存储中的工作负载优化数据库](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md)。
   

## <a name="sql-server-database-engine-ctp-11"></a>SQL Server 数据库引擎 (CTP 1.1)

<a name="InMemoryBulletsCtp11"/>
- 对于内存中功能，旁边列出了内存优化表和本机编译函数的其他增强功能，可在[后续文本](#InMemory_CodeSamples)中获取代码示例：
    - 支持内存优化表中的计算列，包括计算列上的索引。
    - 在本机编译模块和检查约束中对 JSON 函数的完全支持。
    - 本机编译模块中的 `CROSS APPLY` 运算符。   
- 增加了新的字符串函数 [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)、[TRANSLATE](../../t-sql/functions/translate-transact-sql.md) 和 [TRIM](../../t-sql/functions/trim-transact-sql.md)。   
- `WITHIN GROUP` 子句现在支持 [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) 函数。
- 增加了两个新的日语排序规则系列 (Japanese_Bushu_Kakusu_140 and Japanese_XJIS_140)，并增加了在日语排序规则中使用的排序规则选项 Variation-selector-sensitive (_VSS)。 有关详细信息，请参阅[排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)   
- 新的批量访问选项（[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md)）允许直接从如下两种文件访问数据：指定为 CSV 格式的文件，以及通过[外部数据源](../../t-sql/statements/create-external-data-source-transact-sql.md)的新 `BLOB_STORAGE` 选项存储在 Azure Blob 存储中的文件。


## <a name="sql-server-database-engine-ctp-10"></a>SQL Server 数据库引擎 (CTP 1.0)

- 数据库 **COMPATIBILITY_LEVEL** 140 已添加。   在此级别上运行的客户将获得最新语言功能和查询优化器行为。 这包括每个 Microsoft 发布的预发布版本中的更改。
- 对计算增量统计信息更新阈值的方式的改进（需要&140; 兼容模式）。
- [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) 已添加。
- 已将许多性能和语言增强功能添加到内存中表：
    - 内存中表目前不支持 `sp_spaceused`。
    - 本机模块目前支持 `sp_rename`。
    - 本机模块目前支持 `CASE` 语句。
    - 内存中表上 8 个索引的限制已取消。
    - 本机模块中目前支持 `TOP (N) WITH TIES`。
    - 在某些情况下，针对内存中表的 `ALTER TABLE` 现在要快得多。
    - 现可并行执行事务重做内存中表。 这大大减少了进行故障转移的时间，或在某些情况下重启的时间。
    - 内存中检查点文件现可存储在 Azure 存储中。 与已具有此功能的 LDF 文件相比，这将为 MDF 提供等效的功能。
- 聚集列存储索引现支持 LOB 列 (nvarchar(max)、varchar(max)、varbinary(max))。
- 已添加 [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md) 聚合函数。  
- 新权限：`DATABASE SCOPED CREDENTIAL` 当前属于安全对象类，可支持 `CONTROL`、`ALTER`、`REFERENCES`、`TAKE OWNERSHIP` 和 `VIEW DEFINITION` 权限。 现可在 `sys.fn_builtin_permissions` 中查看仅限于 SQL 数据库的 `ADMINISTER DATABASE BULK OPERATIONS`。   
- 添加了 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) DMV，为 Windows 和 Linux 提供操作系统信息。   
- 使用 R Services 创建数据库角色，以管理与包关联的权限。 有关详细信息，请参阅 [SQL Server 的 R 包管理](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。
 
<a name="InMemory_CodeSamples"/> 
## <a name="code-samples-for-new-in-memory-enhancements"></a>新的内存中增强功能的代码示例

以下各小节提供 Transact-SQL 代码示例，这些示例对本文前面的文本中按项目符号列出的新内存中功能进行了说明。

可在[此处](#InMemoryBulletsCtp11)查看有关内存中的 CTP 1.1 项目符号列表。

#### <a name="computed-column-in-a-memory-optimized-table"></a>内存优化表中的计算列

此 CREATE TABLE 语句说明了前面文本中提到的关于 CTP 1.1 的以下功能：

- 列上的 JSON 检查约束。
- 新的计算列。
- 计算列上的索引。

```tsql
CREATE TABLE Product(
    ProductID  int            PRIMARY KEY NONCLUSTERED,
    Name       nvarchar(400)  NOT NULL,
    Price      float,

    Data      nvarchar(4000)  CONSTRAINT [Data contains JSON]  CHECK (ISJSON(Data)=1),

    MadeIn  AS CAST(JSON_VALUE(Data, '$.MadeIn')            as NVARCHAR(50)) PERSISTED,
    Cost    AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float       ),

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)
)
        WITH (MEMORY_OPTIMIZED=ON);
```

#### <a name="cross-apply-and-json-functions"></a>CROSS APPLY 和 JSON 函数

对于本机编译的存储过程，此 CREATE PROCEDURE 语句说明了前面文本中提到的关于 CTP 1.1 的以下功能：

- CROSS APPLY 运算符。
- JSON 函数。

```tsql
CREATE OR ALTER PROCEDURE ProductList()
    WITH SCHEMABINDING, NATIVE_COMPILATION
as begin
    atomic with (transaction isolation level = snapshot,  language = N'English')

    SELECT
            ProductID, Name, Price, Tags,
            Data,
            JSON_VALUE(Data,'$.MadeIn') AS MadeIn,
            value
        FROM Product
        CROSS APPLY OPENJSON(Data, '$.SalesReasons')
        FOR JSON PATH
end;
```
