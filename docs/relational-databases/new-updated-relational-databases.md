---
title: "已更新-关系数据库文档 |Microsoft 文档"
description: "显示有关在最近更改文档，关系数据库的更新内容的代码段。"
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
ms.date: 07/17/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 71203bfa7cb4dcd06cc14ad8e49e5bc1113f8605
ms.openlocfilehash: 519fbd2bc596112dbb1c662d76e4aeeb230ffc36
ms.contentlocale: zh-cn
ms.lasthandoff: 07/19/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新的和最近的更新： 关系数据库文档



几乎每日 Microsoft 及其现有的文章的一些上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文档网站。 这篇文章显示摘录最近已更新的文章。 可能还会列出链接到新的文章。

定期重新运行程序生成这篇文章。 有时摘录可使用不完善格式，或出现 markdown 源文章中的说明。 此处永远不会显示图像。

报告的以下日期范围和主题的新的更新：



- 更新日期范围：&nbsp;从 2017-05-23&nbsp; 到 2017-07-17&nbsp;
- *主题区域：* &nbsp; **关系数据库**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [Server 2016 的 SQL Server 内存中 OLTP 内部组件](in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016.md)
2. [SQL 数据库中的自适应查询处理](performance/adaptive-query-processing.md)
3. [增强隐私和使用 Microsoft SQL 平台解决 GDPR 要求的指南](security/microsoft-sql-and-the-gdpr-requirements.md)
4. [sys.pdw_replicated_table_cache_state (Transact-SQL)](system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql.md)
5. [sys.trusted_assemblies (Transact-SQL)](system-catalog-views/sys-trusted-assemblies-transact-sql.md)
6. [sys.dm_exec_query_parallel_workers (Transact-SQL)](system-dynamic-management-views/sys-dm-exec-query-parallel-workers-transact-sql.md)
7. [sys.sp_add_trusted_assembly (Transact-SQL)](system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)
8. [sys.sp_drop_trusted_assembly (Transact-SQL)](system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact 的最近更新的文章的列表

此紧凑列表提供了在摘要部分列出的所有更新文章的链接。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>与摘录更新的文章

此部分显示的摘自从最近出现了大规模更新的文章中收集的更新。

此处显示的摘自其正确的语义上下文的来自分隔。 此外，有时摘录分开环绕在实际的文章中的重要的 markdown 语法。 因此这些摘录适用于一般性指导原则。 摘录仅使你能够知道您的兴趣是否值得花些时间后，单击，访问实际的文章。

有关这些和其他原因，不从这些摘录中，复制代码并不会为确切真实任何文本摘录。 相反，请访问实际的文章。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-altering-memory-optimized-tablesin-memory-oltpaltering-memory-optimized-tablesmd"></a>1.&nbsp; [更改内存优化表](in-memory-oltp/altering-memory-optimized-tables.md)

更新日期：2017-06-23 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[下一篇](#TitleNum_2)）

<!-- Source markdown line 82.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8359700b5db24838f1bb273526794c2865bbbe11 41d77cf0bbcf53a1b64d6524a24e5736c5a073da  (PR=2171  ,  Filename=altering-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**记录内存优化表上的 ALTER TABLE**

在一个内存优化表中，大多数 ALTER TABLE 方案可同时运行，从而优化了向事务日志的写入。 这种优化是通过只将元数据更改记入事务日志中来实现的。 但是，以下 ALTER TABLE 操作将以单线程运行，而未经过日志优化。

本示例中的单线程操作会将改变表的整个内容都记录到事务日志中。 单线程操作的列表如下：

- 更改或添加列以使用大型对象 (LOB) 类型：nvarchar(max)、varchar(max) 或 varbinary(max)。

- 添加或删除列存储索引。

- 影响 [off-row column--../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) 的几乎任何内容。

    - 导致行上列移动行外列。

    - 导致行外列移动行上列。

    - 创建新的行外列。

    - *异常：* 已使用优化方式记录了延长行外列。 
  




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-table-and-row-size-in-memory-optimized-tablesin-memory-oltptable-and-row-size-in-memory-optimized-tablesmd"></a>2.&nbsp; [内存优化表中的表和行大小](in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)

更新日期：2017-06-22 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_1) | [下一篇](#TitleNum_3)）

<!-- Source markdown line 114.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 27ce0fa2e7bb464f9c3d6e32dd195de3b79abfcd 0a3cacd86024e2b734704ffd37e55ca0b17a0c94  (PR=2163  ,  Filename=table-and-row-size-in-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=fe6de2b16b9792a5399b1c014af72a2a5ee52377) -->



 
  
 [行正文大小] 的计算在下表中讨论。  
  
 对于行正文大小，有两种不同的计算：计算大小和实际大小。  
  
-   计算大小表示为 [计算行正文大小]，用于确定是否超出了 8,060 字节的行大小限制。  
  
-   实际大小表示为 [实际行正文大小]，是行正文在内存和检查点文件中的实际存储大小。  
  
 [计算行正文大小] 和 [实际行正文大小] 的计算方式相似。 唯一的区别是 (n)varchar(i) 和 varbinary(i) 列大小的计算，如下表底部所示。 计算行正文大小使用声明的大小 *i* 作为列大小，而实际行正文大小使用实际数据大小。  
  
 下表介绍行正文大小的计算，公式为 [实际行正文大小] = SUM([浅表类型的大小]) + 2 + 2 * [深表类型列数]。  
  
|章节|Size|注释|  
|-------------|----------|--------------|  
|浅表类型列|SUM([浅表类型的大小])。 各类型的大小（字节数）如下：<br /><br /> **Bit**：1<br /><br /> **Tinyint**：1<br /><br /> **Smallint**：2<br /><br /> **Int**：4<br /><br /> **Real**：4<br /><br /> **Smalldatetime**：4<br /><br /> **Smallmoney**：4<br /><br /> **Bigint**：8<br /><br /> **Datetime**：8<br /><br /> **Datetime2**：8<br /><br /> **Float**：8<br /><br /> **Money**：8<br /><br /> **Numeric**（精度 <= 18）：8<br /><br /> **Time**：8<br /><br /> **Numeric**（精度 > 18）：16<br /><br /> **Uniqueidentifier**：16||  
|浅表列填充|可能的值有：<br /><br /> 如果存在深表类型列并且浅表列的总数据大小是奇数，则为 1。<br /><br /> 否则为 0|深表类型为类型 (var)binary 和 (n)(var)char。|  




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-post-migration-validation-and-optimization-guidepost-migration-validation-and-optimization-guidemd"></a>3.&nbsp; [迁移后验证和优化指南](post-migration-validation-and-optimization-guide.md)

更新日期：2017-06-21 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_2) | [下一篇](#TitleNum_4)）

<!-- Source markdown line 27.  ms.author= "harinid".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 faa2e3dd8be3aeb475bf8c7f71617ebf17969892 f2760dfecda10baeb121929b72a4d8164e81185b  (PR=2126  ,  Filename=post-migration-validation-and-optimization-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=dcbeda6b8372b358b6497f78d6139cad91c8097c) -->



以下是迁移到 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 平台后遇到的一些常见性能方案和解决方法。 包括特定于 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 到 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 迁移（旧版本到新版本），以及外部平台（如 Oracle、DB2、MySQL 和 Sybase）到 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 迁移的方案。

<a name="CEUpgrade"></a>**由于 CE 版本变更导致的查询回归**


适用对象：[!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 到 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 的迁移。

如果从较旧版 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 迁移到 [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] 或更高版本，并将 [数据库兼容性级别--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 升级为最新版，则工作负荷可能面临性能下降的风险。

这是因为，自 [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] 起，所有查询优化器更改都会绑定到最新的 [数据库兼容性级别--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)，因此计划不会在升级后立即更改，而是在用户将 `COMPATIBILITY_LEVEL` 数据库更改为最新版本后更改。 利用此功能和 Query Store，你可以在升级过程中对查询性能进行精确的控制。 

若要详细了解 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中引入的查询优化器变更，请参阅[使用 SQL Server 2014 基数估算器优化查询计划](http://msdn.microsoft.com/library/dn673537.aspx)。




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sysquerystoreplan-transact-sqlsystem-catalog-viewssys-query-store-plan-transact-sqlmd"></a>4. &nbsp; [sys.query_store_plan (Transact-SQL)](system-catalog-views/sys-query-store-plan-transact-sql.md)

更新日期：2017-06-05 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[上一篇](#TitleNum_3)）

<!-- Source markdown line 58.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1b77e34309ba7033578b3c82ed83c8c2fbc93e24 ce4ade9ab906c35cb87068a1fb91c4e1d7549aac  (PR=1940  ,  Filename=sys-query-store-plan-transact-sql.md  ,  Dirpath=docs\relational-databases\system-catalog-views\  ,  MergeCommitSha40=1d363db8e8bd0e1460cdea3c3a7add68e48714c9) -->



**计划强制限制**

查询存储中具有一种可用于强制查询优化器使用特定执行计划的机制。 但是，有些限制可能会阻止计划强制执行。 

首先，计划是否包含以下构造：
* INSERT BULK 语句。
* INSERT BULK 语句。
* 对外部表的引用
* 分布式查询或全文操作
* 使用全局查询 
* 游标
* 无效的星型联接规范 

其次，计划依赖的对象何时不再可用：
* 数据库（计划来自的数据库不再存在时）
* 索引（不再存在或已禁用）

最后，计划本身的问题：
* 用于查询不合法
* 查询优化器超出了允许的操作数
* 格式不正确的计划 XML





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>类似文章

本节针对同一 GitHub.com 存储库 ([MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/)) 中其他主题区域的最近更新的文章列出了非常相似的文章。

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新的和更新的文章 (4+4)：Advanced Analystics for SQL 文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新的和更新的文章 (2+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (1+2)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新的和更新的文章 (6+0)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新的和更新的文章 (13+2)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新的和更新的文章 (1+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (1+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (8+4)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新的和更新的文章 (2+2)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新的和更新的文章 (1+0)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)
- [新的和更新的文章 (0+1)：Tools for SQL 文档](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新的和更新的文章 (0+0)：Integration Services for SQL 文档](../integration-services/new-updated-integration-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：Reporting Services for SQL 文档](../reporting-services/new-updated-reporting-services.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


&nbsp;


